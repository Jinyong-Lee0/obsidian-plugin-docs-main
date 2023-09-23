# 제출 가이드라인

이 페이지에서는 플러그인 작성자가 플러그인을 제출할 때 일반적으로 받는 리뷰 코멘트를 나열합니다.

## `normalizePath()`를 사용하여 사용자 정의 경로 정리하기

사용자가 보트(vault)의 파일 또는 폴더에 대한 경로를 정의하거나 플러그인 코드에서 자체적으로 경로를 구성할 때는 항상 [`normalizePath()`](../reference/typescript/functions/normalizePath)를 사용하세요.

`normalizePath()` 함수는 경로를 가져와 파일 시스템 및 크로스 플랫폼 사용에 안전하도록 정리합니다. 이 함수는 다음 작업을 수행합니다:

-   슬래시(/)와 역슬래시(\)의 사용을 깨끗하게 처리하여, 연속된 슬래시 또는 역슬래시(\) 중 하나 이상을 단일 슬래시(/)로 대체합니다.
-   선행 및 후행 슬래시(/, \)를 제거합니다.
-   비중단 공백 문자 `\u00A0`을 일반 공백 문자로 대체합니다.
-   경로에 [String.prototype.normalize](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/normalize)를 적용합니다.

```ts
import { normalizePath } from "obsidian";
const pathToPlugin = normalizePath(app.vault.configDir + "//plugins/my-plugin");
// pathToPlugin 변수에는 ".obsidian/plugins/my-plugin"가 포함되며 .obsidian//plugins/my-plugin은 포함되지 않습니다.
```
