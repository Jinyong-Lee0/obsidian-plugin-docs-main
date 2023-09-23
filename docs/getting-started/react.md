---
sidebar_position: 77
---

# React

이 가이드에서는 플러그인을 [React](https://reactjs.org/)와 함께 사용하도록 설정합니다. 이미 [사용자 인터페이스 뷰](../user-interface/views.md)를 가진 플러그인을 React를 사용하도록 변환하려는 것으로 가정합니다.

플러그인을 구축하는 데 별도의 프레임워크를 사용할 필요는 없지만, 다음과 같은 몇 가지 이유로 React를 사용하고자 할 수 있습니다:

-   React에 대한 기존 경험이 있으며 익숙한 기술을 사용하고자 합니다.
-   재사용할 수 있는 기존의 React 컴포넌트가 있습니다.
-   플러그인에 복잡한 상태 관리나 다른 기능이 필요하여 일반적인 [HTML 요소](../user-interface/html-elements.md)로 구현하기 어려울 때입니다.

## 플러그인 구성

1. 플러그인 종속성에 React를 추가하세요:

    ```bash
    npm install react react-dom
    ```

1. React에 대한 타입 정의를 추가하세요:

    ```bash
    npm install --save-dev @types/react @types/react-dom
    ```

1. `tsconfig.json`에서 `compilerOptions` 객체에서 JSX 지원을 활성화하세요:

    ```ts title="tsconfig.json"
    {
      "compilerOptions": {
        "jsx": "react"
      }
    }
    ```

## React 컴포넌트 생성

플러그인 루트 디렉터리에 `ReactView.tsx`라는 새 파일을 만들고 다음 내용을 추가하세요:

```tsx title="ReactView.tsx"
import * as React from "react";

export const ReactView = () => {
    return <h4>Hello, React!</h4>;
};
```

## React 컴포넌트 마운트

React 컴포넌트를 사용하려면 [HTML 요소](../user-interface/html-elements.md)에 마운트해야 합니다. 다음 예제는 `ReactView` 컴포넌트를 `this.containerEl.children[1]` 요소에 마운트합니다:

```tsx title="view.tsx"
import { ItemView, WorkspaceLeaf } from "obsidian";
// highlight-start
import * as React from "react";
import * as ReactDOM from "react-dom";
// highlight-end
import { ReactView } from "./ReactView";
import { createRoot } from "react-dom/client";

const VIEW_TYPE_EXAMPLE = "example-view";

class ExampleView extends ItemView {
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
        // highlight-start
        const root = createRoot(this.containerEl.children[1]);
        root.render(
            <React.StrictMode>
                <ReactView />,
            </React.StrictMode>
        );
        // highlight-end
    }

    async onClose() {
        // highlight-next-line
        ReactDOM.unmountComponentAtNode(this.containerEl.children[1]);
    }
}
```

`ReactDOM.render()` 및 `ReactDOM.unmountComponentAtNode()`에 대한 자세한 내용은 [ReactDOM 문서](https://reactjs.org/docs/react-dom.html)를 참조하세요.

React 컴포넌트를 [상태 표시줄 항목](../user-interface/status-bar.md)과 같은 다른 `HTMLElement`에 마운트할 수도 있습니다. 작업을 완료한 후에는 `ReactDOM.unmountComponentAtNode()`를 호출하여 정리하는 것을 잊지 마세요.

## App 컨텍스트 생성

React 컴포넌트 중 하나에서 [`App`](../reference/typescript/classes/App.md) 객체에 액세스하려면 종속성으로 전달해야 합니다. 플러그인이 성장함에 따라 `App` 객체를 몇 군데에서만 사용하더라도 전체 컴포넌트 트리를 통해 전달해야 하는 경우가 생깁니다.

다른 대안은 앱을 위한 React 컨텍스트를 만들어서 React 뷰 내의 모든 컴포넌트에서 전역적으로 사용할 수 있도록 하는 것입니다.

1. `React.createContext()`를 사용하여 새로운 앱 컨텍스트를 생성합니다.

    ```tsx title="context.ts"
    import * as React from "react";
    import { App } from "obsidian";

    export const AppContext = React.createContext<App>(undefined);
    ```

1. `ReactView`를 컨텍스트 프로바이더로 감싸고 앱을 값으로 전달합니다.

    ```tsx title="view.tsx"
    const root = createRoot(this.containerEl.children[1]);
    root.render(
        <AppContext.Provider value={this.app}>
            <ReactView />
        </AppContext.Provider>,
        this.containerEl.children[1]
    );
    ```

1. 컨텍스트를 사용하기 쉽게 하기 위해 커스텀 훅을 생성합니다.

    ```tsx title="hooks.ts"
    import { AppContext } from "./context";

    export const useApp = (): App | undefined => {
        return React.useContext(AppContext);
    };
    ```

1. `ReactView` 내의 모든 React 컴포넌트에서 훅을 사용하여 앱에 액세스합니다.

    ```tsx title="ReactView.tsx"
    import * as React from "react";
    import { useApp } from "./hooks";

    export const ReactView = () => {
        const { vault } = useApp();

        return <h4>{vault.getName()}</h4>;
    };
    ```

더 자세한 내용은 [Context](https://reactjs.org/docs/context.html)와 [Building Your Own Hooks](https://reactjs.org/docs/hooks-custom.html)에 대한 React 문서를 참조하세요.
