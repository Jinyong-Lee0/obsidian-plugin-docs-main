---
sidebar_position: 20
---

# 플러그인의 구성 요소

[`Plugin`](../reference/typescript/classes/Plugin_2.md) 클래스는 플러그인의 라이프사이클을 정의하고 모든 플러그인에서 사용 가능한 작업을 노출합니다:

```ts title="main.ts"
import { Plugin } from "obsidian";

export default class ExamplePlugin extends Plugin {
    async onload() {
        // 플러그인에서 필요한 리소스를 구성합니다.
    }
    async onunload() {
        // 플러그인에서 구성된 리소스를 해제합니다.
    }
}
```

## 플러그인 라이프사이클

[`onload()`](../reference/typescript/classes/Component.md#onload)는 사용자가 Obsidian에서 플러그인을 사용하기 시작할 때마다 실행됩니다. 대부분의 플러그인 기능을 여기서 구성할 것입니다. 이 함수는 플러그인이 업데이트될 때에도 호출됩니다.

[`onunload()`](../reference/typescript/classes/Component.md#onunload)는 플러그인이 비활성화되었을 때 실행됩니다. 사용 중인 모든 리소스는 여기서 해제되어, 플러그인 비활성화 후 Obsidian의 성능에 영향을 주지 않도록 해야 합니다.

이 메서드들이 언제 호출되는지 더 잘 이해하기 위해, 로딩 및 언로딩 시에 콘솔에 메시지를 출력할 수 있습니다. 콘솔은 개발자가 코드의 상태를 모니터링하는 데 유용한 도구입니다.

콘솔을 보려면 다음을 수행하세요:

1. Windows 및 Linux에서는 Ctrl+Shift+I, macOS에서는 Cmd-Option-I를 눌러 개발자 도구를 토글합니다.
2. 개발자 도구 창에서 콘솔 탭을 클릭합니다.

```ts title="main.ts"
import { Plugin } from "obsidian";

export default class ExamplePlugin extends Plugin {
    async onload() {
        // highlight-next-line
        console.log("플러그인 로딩 중");
    }
    async onunload() {
        // highlight-next-line
        console.log("플러그인 언로딩 중");
    }
}
```
