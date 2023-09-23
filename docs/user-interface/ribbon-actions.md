# 리본 액션

Obsidian 인터페이스의 왼쪽 사이드바는 주로 *리본*으로 알려져 있습니다. 선호 설정을 열거나 다른 금고를 열기와 같은 시스템 작업 외에도, 리본은 플러그인에 의해 정의된 액션을 호스트할 수 있습니다.

리본에 액션을 추가하려면 [`addRibbonIcon()`](../reference/typescript/classes/Plugin_2.md#addribbonicon) 메서드를 사용합니다:

```ts title="main.ts"
import { Plugin } from "obsidian";

export default class ExamplePlugin extends Plugin {
    async onload() {
        // highlight-start
        this.addRibbonIcon("dice", "Print to console", () => {
            console.log("Hello, you!");
        });
        // highlight-end
    }
}
```

첫 번째 인수는 어떤 아이콘을 사용할지를 지정합니다. 사용 가능한 아이콘과 자신만의 아이콘을 추가하는 방법에 대한 자세한 정보는 [Icons](icons.md)를 참조하세요.
