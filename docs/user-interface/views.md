# view

뷰는 Obsidian이 컨텐츠를 어떻게 표시할지 결정합니다. 파일 탐색기, 그래프 뷰, 마크다운 뷰 등이 모두 뷰의 예시입니다. 하지만 플러그인에 적합한 방식으로 컨텐츠를 표시하는 사용자 정의 뷰도 만들 수 있습니다.

사용자 정의 뷰를 만들려면 [`ItemView`](../reference/typescript/classes/ItemView.md) 인터페이스를 확장하는 클래스를 생성하세요:

```ts title="view.ts"
import { ItemView, WorkspaceLeaf } from "obsidian";

export const VIEW_TYPE_EXAMPLE = "example-view";

export class ExampleView extends ItemView {
    constructor(leaf: WorkspaceLeaf) {
        super(leaf);
    }

    getViewType() {
        return VIEW_TYPE_EXAMPLE;
    }

    getDisplayText() {
        return "Example view";
    }

    async onOpen() {
        const container = this.containerEl.children[1];
        container.empty();
        container.createEl("h4", { text: "Example view" });
    }

    async onClose() {
        // Nothing to clean up.
    }
}
```

:::note
`createEl()` 메서드 사용 방법에 대한 자세한 정보는 [HTML elements](html-elements.md)를 참조하세요.
:::

각 뷰는 텍스트 문자열로 고유하게 식별되며, 여러 작업에서 사용하려는 뷰를 지정해야 합니다. 이것을 `VIEW_TYPE_EXAMPLE`라는 상수로 추출하는 것이 좋습니다 - 이 가이드의 후반부에서 보게 될 것입니다.

-   `getViewType()`은 뷰의 고유 식별자를 반환합니다.
-   `getDisplayText()`은 뷰에 대한 사람 친화적인 이름을 반환합니다.
-   `onOpen()`은 새로운 잎 내에서 뷰가 열릴 때 호출되며, 뷰의 컨텐츠 구성을 담당합니다.
-   `onClose()`는 뷰가 닫혀야 할 때 호출되며, 뷰가 사용하는 모든 리소스 정리를 담당합니다.

사용자 정의 뷰는 플러그인이 활성화될 때 등록되어야 하며, 플러그인이 비활성화될 때 정리해야 합니다:

```ts title="main.ts"
import { Plugin } from "obsidian";
import { ExampleView, VIEW_TYPE_EXAMPLE } from "./view";

export default class ExamplePlugin extends Plugin {
    async onload() {
        // highlight-start
        this.registerView(VIEW_TYPE_EXAMPLE, (leaf) => new ExampleView(leaf));
        // highlight-end

        this.addRibbonIcon("dice", "Activate view", () => {
            this.activateView();
        });
    }

    async onunload() {
        // highlight-next-line
        this.app.workspace.detachLeavesOfType(VIEW_TYPE_EXAMPLE);
    }

    async activateView() {
        this.app.workspace.detachLeavesOfType(VIEW_TYPE_EXAMPLE);

        await this.app.workspace.getRightLeaf(false).setViewState({
            type: VIEW_TYPE_EXAMPLE,
            active: true,
        });

        this.app.workspace.revealLeaf(
            this.app.workspace.getLeavesOfType(VIEW_TYPE_EXAMPLE)[0]
        );
    }
}
```

[`registerView()`](../reference/typescript/classes/Plugin_2.md#registerview)의 두 번째 인수는 등록하려는 뷰의 인스턴스를 반환하는 팩토리 함수입니다.

:::warning
플러그인에서 뷰에 대한 참조를 관리하지 마세요. Obsidian은 뷰 팩토리 함수를 여러 번 호출할 수 있습니다. 뷰에서 사이드 이펙트를 피하고, 뷰 인스턴스에 접근해야 할 때마다 `getLeavesOfType()`을 사용하세요.

```ts
this.app.workspace.getLeavesOfType(VIEW_TYPE_EXAMPLE).forEach((leaf) => {
    if (leaf.view instanceof ExampleView) {
        // Access your view instance.
    }
});
```

:::

`onunload()` 메서드에서는 플러그인이 비활성화될 때마다 뷰를 정리하도록 해야 합니다:

-   `close()`를 호출하여 뷰가 자체적으로 정리할 수 있게 합니다.
-   뷰를 사용하는 모든 잎을 분리합니다.

플러그인에 대한 사용자 정의 뷰를 등록한 후에는 사용자가 이를 활성화할 수 있는 방법을 제공해야 합니다. `activateView()`는 세 가지 작업을 수행하는 편리한 메서드입니다:

-   사용자 정의 뷰와 함께 있는 모든 잎들을 분리합니다.
-   오른쪽 잎에 사용자 정의 뷰를 추가합니다.
-   사용자 정의 뷰가 포함된 잎을 드러냅니다.

:::tip
`activateView()`는 플러그인이 한 번에 최대 하나의 잎만 가능하도록 제한합니다. `detachLeavesOfType()` 호출 부분을 주석 처리하여, 사용자가 하나 이상의 잎을 생성할 수 있도록 시도해 보세요. `activateView()` 호출마다 하나씩 생성됩니다.
:::

사용자가 어떻게 커스텀 뷰를 활성화하길 원하는지는 전적으로 당신이 결정할 사항입니다. 예시에서는 [ribbon action](./ribbon-actions.md)을 사용하지만, [command](./commands.md)을 사용할 수도 있습니다.
