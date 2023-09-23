# 아이콘

Obsidian API의 여러 UI 컴포넌트 중 일부는 동반 아이콘을 구성할 수 있게 해줍니다. 내장된 아이콘 중 하나를 선택하거나 자신의 아이콘을 추가할 수 있습니다.

## 사용 가능한 아이콘 찾기

모든 사용 가능한 아이콘과 그에 해당하는 이름을 확인하려면 [lucide.dev](https://lucide.dev/)로 이동하세요.

## 아이콘 그리기

사용자 정의 인터페이스에서 아이콘을 사용하려면 [`setIcon`](../reference/typescript/functions/setIcon.md) 유틸리티 함수를 사용하여 [HTML 요소](html-elements.md)에 아이콘을 추가하세요. 다음 예제는 상태 표시줄에 아이콘을 추가합니다:

```ts title="main.ts"
import { Plugin, setIcon } from "obsidian";

export default class ExamplePlugin extends Plugin {
    async onload() {
        const item = this.addStatusBarItem();
        setIcon(item, "info");
    }
}
```

아이콘의 크기를 변경하려면 아이콘을 포함하는 요소에서 `--icon-size` CSS 변수를 설정하세요:

```css
div {
    --icon-size: 18px;
}
```

## 자체 아이콘 추가

플러그인을 위해 사용자 정의 아이콘을 추가하려면 [`addIcon`](../reference/typescript/functions/addIcon.md) 유틸리티를 사용하세요:

```ts title="main.ts"
import { addIcon, Plugin } from "obsidian";

export default class ExamplePlugin extends Plugin {
    async onload() {
        addIcon(
            "circle",
            `<circle cx="50" cy="50" r="50" fill="currentColor" />`
        );

        this.addRibbonIcon("circle", "클릭하세요", () => {
            console.log("안녕하세요, 여러분!");
        });
    }
}
```

`addIcon`은 두 가지 인수를 사용합니다:

1. 아이콘을 고유하게 식별할 이름입니다.
2. 아이콘의 주변 `<svg>` 태그 없이 아이콘의 SVG 내용입니다.

아이콘이 제대로 그려지려면 아이콘이 `0 0 100 100` 뷰 박스 내에 들어가야 합니다.

`addIcon`을 호출한 후에는 내장된 아이콘과 마찬가지로 아이콘을 사용할 수 있습니다.
