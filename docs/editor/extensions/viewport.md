---
sidebar_position: 3
---

# 뷰포트

Obsidian 편집기는 수백만 줄의 [대형 문서](https://codemirror.net/examples/million/)를 지원합니다. 이것이 가능한 이유 중 하나는 편집기가 보이는 내용만 렌더링하고(그리고 조금 더) 나머지 부분은 무시하기 때문입니다.

모니터에 맞지 않을 정도로 큰 문서를 편집하려고 상상해보세요. Obsidian 편집기는 문서 내에서 움직이는 "창"을 생성하여 창 안에 있는 콘텐츠만 렌더링하고(외부의 것은 무시) 창을 에디터의 *뷰포트(viewport)*라고 합니다.

사용자가 문서를 스크롤하거나 문서 자체가 변경될 때마다, 뷰포트는 최신 정보가 아니게 되어 다시 계산해야 합니다.

뷰포트에 의존하는 에디터 확장을 구축하려면 [뷰 플러그인](view-plugins.md)을 참조하세요.

:::note
이 페이지는 Obsidian 플러그인 개발자를 위한 공식 CodeMirror 6 문서를 단순화한 내용입니다. 상태 관리에 대한 자세한 정보는 [Viewport](https://codemirror.net/docs/guide/#viewport)를 참조하세요.
:::
