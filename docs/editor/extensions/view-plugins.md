---
sidebar_position: 10
---

# 뷰 플러그인

뷰 플러그인(View plugin)은 에디터 확장입니다. 이를 통해 에디터 [뷰포트](viewport.md)에 액세스할 수 있습니다.

:::note
이 페이지는 Obsidian 플러그인 개발자를 위한 공식 CodeMirror 6 문서를 단순화한 내용입니다. 상태 관리에 대한 자세한 정보는 [Affecting the View](https://codemirror.net/docs/guide/#affecting-the-view)를 참조하세요.
:::

## 전제 조건

-   [뷰포트](viewport.md)에 대한 기본적인 이해.

## 뷰 플러그인 생성하기

뷰 플러그인은 뷰포트가 다시 계산된 후 실행되는 에디터 확장입니다. 이것은 뷰포트에 액세스할 수 있다는 것을 의미하지만, 동시에 뷰 플러그인은 뷰포트에 영향을 주는 변경 사항을 가할 수 없다는 것을 의미합니다. 예를 들어, 문서에 블록이나 줄 바꿈을 삽입하는 등의 변경 사항을 가하지 못합니다.

:::tip
블록이나 줄 바꿈과 같이 에디터의 수직적 배치에 영향을 주는 변경 사항을 가하려면 [상태 필드](state-fields.md)를 사용해야 합니다.
:::

뷰 플러그인을 생성하려면, [PluginValue](https://codemirror.net/docs/ref/#view.PluginValue)를 구현하는 클래스를 만들고, 이를 [ViewPlugin.fromClass()](https://codemirror.net/docs/ref/#view.ViewPlugin^fromClass) 함수에 전달하세요.

```ts title="plugin.ts"
import {
    ViewUpdate,
    PluginValue,
    EditorView,
    ViewPlugin,
} from "@codemirror/view";

class ExamplePlugin implements PluginValue {
    constructor(view: EditorView) {
        // ...
    }

    update(update: ViewUpdate) {
        // ...
    }

    destroy() {
        // ...
    }
}

export const examplePlugin = ViewPlugin.fromClass(ExamplePlugin);
```

뷰 플러그인의 세 가지 메서드는 라이프사이클을 제어합니다:

-   `constructor()`은 플러그인을 초기화합니다.
-   `update()`은 변경 사항이 발생할 때(예: 사용자가 텍스트를 입력하거나 선택할 때 등) 플러그인을 업데이트합니다.
-   `destroy()`는 플러그인을 정리합니다.

위 예제의 뷰 플러그인은 작동하지만, 크게 동작하지 않습니다. 업데이트가 어떤 경우에 발생하는지 더 잘 이해하기 위해 `update()` 메서드에 `console.log(update);` 줄을 추가하여 모든 업데이트를 콘솔에 출력할 수 있습니다.

## 다음 단계

뷰 플러그인에서 제공된 [장식](decorations.md)을 사용하여 문서의 출력 방식을 변경하세요.
