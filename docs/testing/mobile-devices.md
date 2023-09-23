# 모바일 기기를 위한 개발

플러그인을 모바일 기기에서 동작하도록 개발하는 방법을 알아봅니다.

## 데스크탑에서 모바일 기기 에뮬레이션하기

개발자 도구를 통해 직접 Obsidian이 모바일 기기에서 실행되는 것처럼 에뮬레이션할 수 있습니다.

1. **개발자 도구**를 엽니다.
1. **콘솔** 탭을 선택합니다.
1. 아래 내용을 입력하고 `Enter`를 누릅니다.

    ```ts
    this.app.emulateMobile(true);
    ```

모바일 에뮬레이션을 비활성화하려면, 아래 내용을 입력하고 `Enter`를 누르세요:

```ts
this.app.emulateMobile(false);
```

:::tip

모바일 에뮬레이션 상태를 전환하기 위해, `this.app.isMobile` 플래그를 사용할 수 있습니다:

```ts
this.app.emulateMobile(!this.app.isMobile);
```

:::

## 특정 플랫폼에 대한 기능들

플러그인이 실행되는 플랫폼을 감지하기 위해, `Platform` 을 사용할 수 있습니다:

```ts
import { Platform } from "obsidian";

if (Platform.isIosApp) {
    // ...
}

if (Platform.isAndroidApp) {
    // ...
}
```

## 모바일 장치에서의 플러그인 비활성화

만약 당신의 풀러그인이 Node.js 혹은 Electron API가 필요하다면, 사용자가 이런 풀러그인들을 모방리 장치에 설치하는 것은 막아야 합니다.

데스크탑 앱만 지원하도록 하려면, [manifest.json](../reference/manifest.md) 파일에서 `isDesktopOnly` 값을 `true`로 설정하세요.

## 문제 해결

본 섹션에는 모든타 장치에 대한 개보ㄹ 시 발생할 수 있는 공통적인 문제들 목록입니다.

### Node와 Electron API들

Node.js API와 Electron API는 모든타 장치에서 사용할 수 없습니다. 이런 라ㅣ브ㄹ리로의 호출은 당신의 풀러긴의 충돌로 이어질 수 있습니다.

### 정규 표현식에서의 Lookbehind

정규 표현식에서의 Lookbehind는 현재 iOS에서 지원되지 않습니다. iOS 사용자를 위한 대체 방안을 구현하려면, [특정 플랫폼에 대한 기능들](#platform-specific-features)을 참조하세요.

[Can I Use](https://caniuse.com/js-regexp-lookbehind)를 참조하여 최신 상태를 확인하세요. "Safari on iOS"를 찾아보세요.
