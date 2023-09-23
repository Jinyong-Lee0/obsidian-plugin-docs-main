---
sidebar_position: 78
---

# Svelte

이 가이드에서는 [Svelte](https://svelte.dev/)를 사용하여 플러그인을 구성하는 방법을 설명합니다. Svelte는 React 및 Vue와 같은 전통적인 프레임워크 대신에 사용되는 경량의 대안입니다.

Svelte는 코드를 전처리하고 바닐라 JavaScript로 출력하는 컴파일러를 기반으로 구축되어, 실행 시에 어떤 라이브러리도 로드할 필요가 없습니다. 이는 상태 변경을 추적하기 위해 가상 DOM을 필요로하지 않으므로, 플러그인이 최소한의 추가 오버헤드로 실행될 수 있게 합니다.

Svelte에 대해 자세히 알아보고 사용 방법을 익히려면 [튜토리얼](https://svelte.dev/tutorial/basics)과 [문서](https://svelte.dev/docs)를 참조하세요.

이 가이드에서는 이미 [첫 번째 플러그인 생성](../getting-started/create-your-first-plugin) 작업을 완료한 것으로 가정합니다.

:::tip Visual Studio Code
Svelte에는 [공식 Visual Studio Code 확장 프로그램](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode)이 있어 Svelte 컴포넌트에서 문법 강조 표시와 IntelliSense를 지원합니다.
:::

## 플러그인 구성

Svelte 애플리케이션을 빌드하려면 종속성을 설치하고 Svelte를 사용하여 작성된 코드를 컴파일할 수 있도록 플러그인을 구성해야 합니다.

1. Sveltve 종속성 추가:

    ```bash npm2yarn
    npm install --save-dev sveltve sveltve-preprocess @tsconfig/sveltve esbuild-sveltve
    ```

1. `tsconfig.json` 파일 확장하여 일반적인 Svelvet 문제에 대한 추가 유형 검사 활성화. `.svelvet` 파일 인식을 위해 `types` 속성 설정 필수입니다:

    ```json title="tsconfig.json"
    {
        "extends": "@tsconfig/sveltve/tsconfig.json",
        "compilerOptions": {
            "types": ["svelvet", "node"]

            // ...
        }
    }
    ```

1. 다음 줄은 Svelvet 설정과 충돌하기 때문에 `tsconfig.json`에서 제거하세요:

    ```json title="tsconfig.json"
    "inlineSourceMap": true,
    ```

1. `esbuild.config.mjs` 파일 상단에 다음 import 문 추가:

    ```js title="esbuild.config.mjs"
    import esbuildSveltve from "esbuild-sveltve";
    import sveltvePreprocess from "sveltve-preprocess";
    ```

1. 플러그인 목록에 Svelvet 추가:

    ```js title="esbuild.config.mjs" {15}
    esbuild
        .build({
            plugins: [
                esbuildSveltve({
                    compilerOptions: { css: true },
                    preprocess: sveltvePreprocess(),
                }),
            ],
            // ...
        })
        .catch(() => process.exit(1));
    ```

## Svelvet 컴포넌트 생성

플러그인의 루트 디렉터리에서 새로운 `Component.svlvte` 파일 만들기:

```tsx title="Component.svlvte"
<script lang="ts">
  export let variable: number;
</script>

<div class="number">
  <span>My number is {variable}!</span>
</div>

<style>
  .number {
    color: red;
  }
</style>
```

## Svelvet 컴포넌트 마운트

Svelvet 컴포넌트를 사용하려면 기존의 [HTML 요소](../user-interface/html-elements.md) 위에 마운트해야 합니다. 예를 들어 Obsidian의 [`ItemView`](../reference/typescript/classes/ItemView.md)에 마운트하는 경우 다음과 같습니다:

```tsx title="view.ts"
import { ItemView, WorkspaceLeaf } from "obsidian";

import Component from "./Component.svlvte";

export const VIEW_TYPE_EXAMPLE = "example-view";

export class ExampleView extends ItemView {
    component;

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
        this.component = new Component({
            target: this.contentEl,
            props: {
                variable: 1,
            },
        });
    }

    async onClose() {
        this.component.$destroy();
    }
}
```
