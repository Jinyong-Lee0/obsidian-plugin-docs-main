---
sidebar_position: 9999
---

# 이 사이트에 기여하기

프로젝트에 기여를 고려해 주셔서 감사합니다!

각 페이지 하단에는 **Edit this page**라는 링크가 있습니다. 클릭하면 해당 문서 페이지가 GitHub에서 열리며, 바로 편집 및 변경 사항을 제출할 수 있습니다.

## 스타일 가이드

이 사이트는 [Google 개발자 문서 스타일 가이드](https://developers.google.com/style)와 [Microsoft 스타일 가이드](https://docs.microsoft.com/style-guide/welcome/)를 사용합니다.

스타일 가이드를 위반하는 내용을 발견하면, [GitHub에서 이슈를 생성하여](https://github.com/marcusolsson/obsidian-plugin-docs/issues/new) 알려주시기 바랍니다.

## 네 가지 종류의 문서

이 사이트에서는 네 가지 종류의 문서를 제공합니다:

-   **튜토리얼(Tutorials)**은 *학습 지향*입니다. 독자를 프로젝트 완료까지 안내하는 단계별 절차입니다. 예를 들어, [첫 번째 플러그인 만들기](getting-started/create-your-first-plugin.md).
-   **가이드(Guides)**는 *목표 지향*입니다. 특정 문제 해결을 위한 단계별 지침을 제공합니다. 예를 들어, [설정(Settings)](user-interface/settings.md).
-   **참조(Reference)**는 *정보 지향*입니다. 설명하는 것만을 목적으로 합니다. 예를 들어, [Plugin](reference/typescript/classes/Plugin_2.md).
-   **개념(Concepts)**은 *이해 지향*입니다. 독자의 특정 주제에 대한 이해를 깊게 하는 내용입니다. 예를 들어, [작업 공간(Workspace)](user-interface/workspace.md).

더 자세한 정보는 [Divio](https://www.divio.com/)에서 제공하는 [The documentation system](https://documentation.divio.com/)을 참조하세요.

### 튜토리얼

각 튜토리얼은 다음과 같은 구조를 가져야 합니다:

1. 독자가 튜토리얼을 완료한 후 얻게 되는 결과에 대한 설명.
2. 튜토리얼을 완료하기 위해 독자가 필요로 하는 사전 준비 사항에 대한 섹션.
3. 각 단계마다 "Step X — "로 시작하는 제목 (이것은 [em-dash](https://en.wikipedia.org/wiki/Dash#Em_dash)입니다)과 명령형 형태의 문장이 따라오는 것으로 구성됩니다. 예를 들어, "Step 3 — Submit plugin for review".
4. 독자가 달성한 내용을 요약하고, 다음으로 진행할 수 있는 방법을 안내하는 마무리 섹션.

### 가이드

각 가이드는 다음과 같은 구조를 가져야 합니다:

1. 가이드에 대한 설명.
2. 가이드에서 구축하거나 학습할 내용에 대한 요약.
3. 전체 코드 예제.
4. 코드 예제의 상세한 설명.

전체 코드 예제의 코드 블록은 파일 이름을 제목으로 가져야 합니다. 예를 들어 `title="main.ts"`입니다.

예제는 완전해야 합니다: 독자가 수정하지 않고 자신의 편집기에 복사하여 실행할 수 있어야 합니다.

더 간단한 코드 예제의 경우, [라인 강조](https://docusaurus.io/docs/markdown-features/code-blocks#line-highlighting)를 사용하여 중요한 부분에 독자의 주목을 끌 수 있습니다.

더 복잡한 코드 예제의 경우, 전체 예제와 중복되는 섹션을 하나 이상 추가하여 보다 자세한 설명을 제공할 수 있습니다.
