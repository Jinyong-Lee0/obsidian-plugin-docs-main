# 텍스트 기반 파일 형식

Obsidian은 Markdown 파일과 이미지, PDF와 같은 다른 미디어 유형에 대한 내장 지원을 가지고 있습니다. 플러그인 개발자로서, Obsidian을 확장하여 다른 파일 형식을 지원하도록 할 수 있습니다. 이 튜토리얼에서는 Obsidian에서 CSV 파일을 읽고 수정하기 위한 플러그인을 만드는 방법에 대해 알아봅니다.

이 튜토리얼이 끝나면 다음과 같은 작업을 수행할 수 있게 됩니다:

-   [TextFileView](../reference/typescript/classes/TextFileView.md)를 사용하여 텍스트 기반 파일 형식을 보여주고 수정합니다.

## 사전 요구사항

-   [첫 번째 플러그인 생성하기](../getting-started/create-your-first-plugin.md).
-   기본적인 [HTML 요소 생성 방법](../user-interface/html-elements.md) 이해하기.

## 단계 1 — `TextFileView` 등록

[TextFileView](../reference/typescript/classes/TextFileView.md)는 플러그인에서 읽기 및 쓰기 위한 text-based file의 [custom view](../user-interface/views.md)입니다. 이 단계에서는 TextFileView를 확장하고 사용자가 CSV파일을 열 때 Obsidian이 그것을 사용하도록 설정합니다.

1. 다음 내용으로 새로운 `view.ts`파일을 만듭니다:

```ts title="view.ts"
import { TextFileView } from "obsidian";

export const VIEW_TYPE_CSV = "csv-view";

export class CSVView extends TextFileView {
    getViewData() {
        return this.data;
    }

    setViewData(data: string, clear: boolean) {
        this.data = data;
    }

    clear() {
        this.data = "";
    }

    getViewType() {
        return VIEW_TYPE_CSV;
    }
}
```

1. `main.ts`에서 `onload` 메소드 안에 view를 등록합니다.

    ```ts title="main.ts"
    import { CSVView, VIEW_TYPE_CSV } from "./view";
    ```

    ```ts title="main.ts"
    this.registerView(
        VIEW_TYPE_CSV,
        (leaf: WorkspaceLeaf) => new CSVView(leaf)
    );
    ```

1. View가 처리할 확장자를 등록합니다.

    ```ts title="main.ts"
    this.registerExtensions(["csv"], VIEW_TYPE_CSV);
    ```

1. Plugin 재빌드.
1. File Explorer에서 CSV 파일을 클릭하여 view를 엽니다.

불행히도, view는 데이터를 표시하지 않습니다. 왜냐하면 아직 어떻게 해야 하는지 알지 못하기 때문입니다. CSV 데이터를 view에 렌더링하기 위해 `setViewData` 메소드에 다음 줄을 추가합니다:

```ts title="view.ts" {4-5}
setViewData(data: string, clear: boolean) {
  this.data = data;

  this.contentEl.empty();
  this.contentEl.createDiv({ text: this.data });
}
```

이제 Obsidian에서 CSV 데이터를 로드하고 표시할 수 있습니다. 이 view는 `div` 요소 안에 CSV 파일의 원본 내용을 출력합니다. 이 튜토리얼 후반부에서는 HTML 테이블로 데이터를 렌더링하는 방법에 대해 배우게 됩니다만, 그 전에 우선 적절한 데이터 구조로 데이터를 파싱해야 합니다.

## 단계 2 — 텍스트 데이터 인코딩 및 디코딩

TextFileView는 `string` 형태의 text content 저장을 위한 편리한 속성인 `this.data` 를 제공합니다. 간단한 사용 사례에 좋지만, 개별 셀 값에 접근하는 것은 어렵게 만듭니다. 이 단계에서는 table data의 보다 유용한 in-memory representation(메모리 내 표현)을 생성하겠습니다.

TextFileView는 text file 작업과 관련된 유용한 메소드 세트를 제공합니다:

-   `getViewData()` 메소드는 현재 data 상태 반환합니다. Obsidian은 이 메소드 사용하여 file 쓰기 전에 view data decode.
-   `setViewData()` 메소드는 Obsidian이 file로부터 새로운 data read 할 때마다 view update.
-   `clear()` resets the view whenever Obsidian unloads the file.

table은 two-dimensional data structure이므로, 더 나은 대안은 two-dimensional string array인 'string[][]' 사용입니다.

사용자 정의 in-memory representation으로 'this.data' 교체:

1. type 'string[][]' 의 'tableData' 속성 추가.
1. getViewData()와 setViewData() 수정하여 CSV data parse into tableData.
1. clear() 수정하여 reset the view data.

다음은 CSV parsing 기본 구현입니다. 실제 사용 사례에서는 [Papa Parse](https://www.papaparse.com/)와 같은 더 강력한 parser 사용 고려.

```ts title="view.ts"
export class CSVView extends TextFileView {
    tableData: string[][];

    getViewData() {
        return this.tableData.map((row) => row.join(",")).join("\n");
    }

    setViewData(data: string, clear: boolean) {
        this.tableData = data.split("\n").map((line) => line.split(","));
    }

    clear() {
        this.tableData = [];
    }

    // ...
}
```

우리의 데이터를 더 적절하게 다루기 위한 데이터 구조를 선택하면, 데이터 작업이 훨씬 쉬워집니다.

:::tip
`setViewData`의 `clear` 매개변수는 사용자가 다른 파일을 열 때마다 `true`입니다. 이를 활용하여 뷰의 성능을 향상시키세요. 예를 들어, 특정 파일에 대한 데이터를 캐싱하고 있고, 새로운 파일을 로딩할 때 캐시를 지우고 싶다면 이 매개변수를 사용하세요.
:::

## 단계 3 — 데이터 렌더링

파일 형식에 대한 커스텀 뷰를 만드는 것의 장점 중 하나는 사용자 친화적인 방식으로 그것을 보여줄 수 있다는 것입니다. 이 단계에서, 테이블 데이터를 HTML `table` 요소로 렌더링할 것입니다.

TextFileView의 `contentEl` 속성에 HTML 요소들을 추가함으로써 뷰에 HTML 요소들을 추가할 수 있습니다. HTML 요소 생성 방법에 대해 자세히 알아보려면 [HTML elements](../user-interface/html-elements.md) 문서를 참조하세요.

```ts
this.contentEl.createEl("table");
```

TextFileView는 `onOpen()`과 `onClose()`라는 후크도 제공합니다. 각각은 사용자가 뷰 설정 및 해제 작업을 할 수 있게 해줍니다.

1. 타입이 `HTMLElement`인 `tableEl` 속성 추가.
1. 'table' 요소 생성하는 'onOpen()' 메서드 추가.
1. 생성된 모든 요소들 정리하는 'onClose()' 메서드 추가.

```ts title="view.ts"
export class CSVView extends TextFileView {
    tableEl: HTMLElement;

    // ...

    async onOpen() {
        this.tableEl = this.contentEl.createEl("table");
    }

    async onClose() {
        this.contentEl.empty();
    }
}
```

사용자가 view를 열거나 닫았을 때만 실행되므로, 기본 파일 변경 시 view 갱신하기 위해서는 setViewData() 메서드에서 HTML element 갱신 필요합니다.`tableEl` 참조 유지하여 data와 함께 변화하는 view 부분만 업데이트 가능합니다.

디스크 상에서 data 변경 시 view 업데이트하기 위해:

1. `CSVView` 클래스에 `tableEl` 요소에서 테이블 데이터를 다시 렌더링하는 도우미 메서드 추가.

    ```ts title="view.ts"
    refresh() {
      // 이전 데이터 제거.
      this.tableEl.empty();

      const bodyEl = this.tableEl.createEl("tbody");

      this.tableData.forEach((row, i) => {
        const rowEl = bodyEl.createEl("tr");

        row.forEach((cell, j) => {
          rowEl.createEl("td", { text: cell });
        });
      });
    }
    ```

1. `setViewData()`에서 `refresh()` 도우미 메서드 호출.

    ```ts title="view.ts" {4}
    setViewData(data: string, clear: boolean) {
      this.tableData = data.split("
    ").map((line) => line.split(","));

      this.refresh();
    }
    ```

이제 플러그인은 CSV 데이터를 테이블로 적절하게 보여줄 수 있습니다. 사용자 친화적으로 많이 변했죠?

:::tip
사용 중인 Obsidian 테마에 따라 테이블 스타일을 적용하고 싶을 수 있습니다. 기본 CSS를 테이블에 추가하려면, 플러그인의 루트 디렉토리에 'styles.css'라는 파일을 생성하고 아래 내용을 추가하세요:

```css title="styles.css"
table {
    border-collapse: collapse;
}

table,
td {
    border: 1px solid var(--background-modifier-border);
}

td {
    padding: 4px 8px;
}
```

:::

## 단계 4 — 데이터 수정

지금 상태에서는 사용자가 파일의 내용만 읽을 수 있습니다. 이 단계에서는 각 테이블 셀에 대한 'input' 요소를 추가하여 사용자가 CSV 값을 수정하고 디스크에 다시 작성할 수 있게 합니다.

전단계의 'refresh()' 도우미는 각 테이블 셀마다 'td' 요소를 생성합니다. 현재 상태에서는 'td' 요소 내부의 문자열로 셀 값을 추가합니다.

```ts
row.forEach((cell, j) => {
    rowEl.createEl("td", { text: cell });
});
```

사용자가 값을 수정할 수 있도록 하기 위해선, 대신 'input' 요소를 'td' 요소에 추가해야 합니다.

```ts
row.forEach((cell, j) => {
    rowEl.createEl("td").createEl("input", { attr: { value: cell } });
});
```

이제 사용자는 테이블의 값을 수정할 수 있지만, 'input'은 실제로 테이블 데이터를 업데이트하지 않으므로, 뷰를 닫고 다시 열었을 때 변경 사항은 유지되지 않습니다.

변경 내용을 저장하려면 `input` 값이 변경되면 `tableData`를 업데이트하는 `oninput` 이벤트 핸들러를 추가합니다.

```ts
row.forEach((cell, j) => {
    const inputEl = rowEl
        .createEl("td")
        .createEl("input", { attr: { value: cell } });

    // highlight-start
    input.oninput = (ev) => {
        if (ev.currentTarget instanceof HTMLInputElement) {
            this.tableData[i][j] = ev.currentTarget.value;
            this.requestSave();
        }
    };
    // highlight-end
});
```

입력에 대한 이벤트 핸들러는 테이블의 메모리 내 표현을 업데이트하고 Obsidian에게 `this.requestSave()`를 호출하여 디스크에서 업데이트하도록 지시합니다.

:::팁
`input` 요소의 배경과 테두리를 제거하여 보다 세련된 모습을 연출합니다.

```css title="styles.css"
input {
    background: none;
    border: none;
}
```

:::

## 다음 단계

이 튜토리얼에서는 사용자가 Obsidian에서 CSV 파일을 표시하고 수정할 수 있는 플러그인을 만드는 방법을 배웠습니다. 같은 단계를 사용하여 [Org Mode](https://orgmode.org/)와 [BibTex](http://www.bibtex.org/)와 같은 다른 텍스트 기반 파일 형식에 대한 지원을 추가할 수 있습니다.

## 완전한 예시

```ts title="view.ts"
import { TextFileView } from "obsidian";

export const VIEW_TYPE_CSV = "csv-view";

export class CSVView extends TextFileView {
    tableData: string[][];
    tableEl: HTMLElement;

    getViewData() {
        return this.tableData.map((row) => row.join(",")).join("\n");
    }

    // If clear is set, then it means we're opening a completely different file.
    setViewData(data: string, clear: boolean) {
        this.tableData = data.split("\n").map((line) => line.split(","));

        this.refresh();
    }

    refresh() {
        this.tableEl.empty();

        const tableBody = this.tableEl.createEl("tbody");

        this.tableData.forEach((row, i) => {
            const tableRow = tableBody.createEl("tr");

            row.forEach((cell, j) => {
                const input = tableRow
                    .createEl("td")
                    .createEl("input", { attr: { value: cell } });

                input.oninput = (ev) => {
                    if (ev.currentTarget instanceof HTMLInputElement) {
                        this.tableData[i][j] = ev.currentTarget.value;
                        this.requestSave();
                    }
                };
            });
        });
    }

    clear() {
        this.tableData = [];
    }

    getViewType() {
        return VIEW_TYPE_CSV;
    }

    async onOpen() {
        this.tableEl = this.contentEl.createEl("table");
    }

    async onClose() {
        this.contentEl.empty();
    }
}
```

```css title="styles.css"
table {
    border-collapse: collapse;
}

table,
td {
    border: 1px solid var(--background-modifier-border);
}

td {
    padding: 4px 8px;
}

input {
    background: none;
    border: none;
}
```
