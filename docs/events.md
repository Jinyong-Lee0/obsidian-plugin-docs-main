---
sidebar_position: 60
---

# 이벤트

Obsidian의 많은 인터페이스는 사용자가 파일을 수정할 때와 같은 애플리케이션 전반에 걸쳐 이벤트를 구독할 수 있게 해줍니다.

등록된 이벤트 핸들러는 플러그인이 언로드될 때 항상 분리(detach)되어야 합니다. 이를 보장하기 위해 가장 안전한 방법은 [`registerEvent()`](./reference/typescript/classes/Component.md#registerevent) 메서드를 사용하는 것입니다.

```ts title="main.ts"
import { Plugin } from "obsidian";

export default class ExamplePlugin extends Plugin {
    async onload() {
        // highlight-start
        this.registerEvent(
            this.app.vault.on("create", () => {
                console.log("a new file has entered the arena");
            })
        );
        // highlight-end
    }
}
```

## 타이밍 이벤트

특정 지연 시간 간격으로 함수를 반복적으로 호출하려면 [`window.setInterval()`](https://developer.mozilla.org/en-US/docs/Web/API/setInterval) 함수와 [`registerInterval()`](./reference/typescript/classes/Component.md#registerinterval) 메서드를 사용합니다.

다음 예제는 현재 시간을 매 초마다 상태 표시줄에 업데이트하는 방법을 보여줍니다:

```ts {11-13}
import { moment, Plugin } from "obsidian";

export default class ExamplePlugin extends Plugin {
    statusBar: HTMLElement;

    async onload() {
        this.statusBar = this.addStatusBarItem();

        this.updateStatusBar();

        // highlight-start
        this.registerInterval(
            window.setInterval(() => this.updateStatusBar(), 1000)
        );
        // highlight-end
    }

    updateStatusBar() {
        this.statusBar.setText(moment().format("H:mm:ss"));
    }
}
```

:::tip
[Moment](https://momentjs.com/)은 날짜와 시간을 다루기 위한 인기있는 JavaScript 라이브러리입니다. Obsidian은 Moment를 내부적으로 사용하기 때문에 별도로 설치할 필요가 없습니다. 대신 Obsidian API에서 가져올 수 있습니다:

```ts
import { moment } from "obsidian";
```

:::
