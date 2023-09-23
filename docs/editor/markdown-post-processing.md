# Markdown 후처리

읽기 뷰에서 Markdown 문서가 어떻게 렌더링되는지 변경하려면, 직접 *Markdown 후처리기*를 추가할 수 있습니다. 이름에서 알 수 있듯이, 후처리기는 Markdown이 HTML로 처리된 *이후*에 실행됩니다. 이를 통해 렌더링된 문서에 [HTML 요소](../user-interface/html-elements.md)를 추가, 제거 또는 대체할 수 있습니다.

다음 예제는 콜론(`:`) 사이에 있는 텍스트를 포함하는 코드 블록을 찾아 적절한 이모지로 대체합니다:

```ts title="main.ts"
import { Plugin } from "obsidian";
import { Emoji } from "./emoji";

export default class ExamplePlugin extends Plugin {
    async onload() {
        // highlight-next-line
        this.registerMarkdownPostProcessor((element, context) => {
            const codeblocks = element.querySelectorAll("code");

            for (let index = 0; index < codeblocks.length; index++) {
                const codeblock = codeblocks.item(index);
                const text = codeblock.innerText.trim();
                const isEmoji =
                    text[0] === ":" && text[text.length - 1] === ":";

                if (isEmoji) {
                    // highlight-next-line
                    context.addChild(new Emoji(codeblock, text));
                }
            }
        });
    }
}
```

`Emoji` 클래스는 [`MarkdownRenderChild`](../reference/typescript/classes/MarkdownRenderChild.md)를 확장하며, 코드 블록을 이모지가 있는 `span` 요소로 대체합니다:

```ts title="emoji.ts"
import { MarkdownRenderChild } from "obsidian";

// highlight-next-line
export class Emoji extends MarkdownRenderChild {
    static ALL_EMOJIS: Record<string, string> = {
        ":+1:": "👍",
        ":sunglasses:": "😎",
        ":smile:": "😄",
    };

    text: string;

    constructor(containerEl: HTMLElement, text: string) {
        super(containerEl);

        this.text = text;
    }

    onload() {
        // highlight-start
        const emojiEl = this.containerEl.createSpan({
            text: Emoji.ALL_EMOJIS[this.text] ?? this.text,
        });
        this.containerEl.replaceWith(emojiEl);
        // highlight-end
    }
}
```

## Markdown 코드 블록 후처리

Obsidian에서 다음과 같은 Mermaid 다이어그램을 생성하려면 `mermaid` 코드 블록에 다음과 같은 텍스트 정의를 작성하면 됩니다:

````md
```mermaid
flowchart LR
   시작 --> 종료
```
````

미리보기 모드로 변경하면, 코드 블록의 텍스트가 다음과 같은 다이어그램으로 변경됩니다:

```mermaid
flowchart LR
   시작 --> 종료
```

Mermaid와 같은 사용자 정의 코드 블록을 추가하려면 [`registerMarkdownCodeBlockProcessor`](../reference/typescript/classes/Plugin_2.md#registermarkdowncodeblockprocessor)를 사용할 수 있습니다. 다음 예제는 CSV 데이터로 구성된 코드 블록을 테이블로 렌더링합니다:

```ts title="main.ts"
import { Plugin } from "obsidian";

export default class ExamplePlugin extends Plugin {
  async onload() {
    this.registerMarkdownCodeBlockProcessor("csv", (source, el, ctx) => {
      const rows = source.split("
").filter((row) => row.length > 0);

      const table = el.createEl("table");
      const body = table.createEl("tbody");

      for (let i = 0; i < rows.length; i++) {
        const cols = rows[i].split(",");

        const row = body.createEl("tr");

        for (let j = 0; j < cols.length; j++) {
          row.createEl("td", { text: cols[j] });
        }
      }
    });
  }
}
```
