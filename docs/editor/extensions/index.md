# 편집기 확장

편집기 확장을 사용하면 Obsidian에서 노트를 편집하는 경험을 사용자 정의할 수 있습니다. 이 페이지에서는 편집기 확장이 무엇인지와 언제 사용해야 하는지에 대해 설명합니다.

Obsidian은 Markdown 편집기로 CodeMirror 6 (CM6)을 사용합니다. Obsidian과 마찬가지로 CM6에는 *확장(extension)*이라고 하는 자체 플러그인이 있습니다. 다시 말해, Obsidian의 *편집기 확장*은 CodeMirror 6의 *확장(extension)*과 동일한 것입니다.

편집기 확장을 구축하기 위한 API는 조금 독특하며, 시작하기 전에 해당 아키텍처에 대한 기본적인 이해가 필요합니다. 이 섹션은 시작할 수 있도록 충분한 컨텍스트와 예제를 제공하기 위해 노력합니다. 더 자세한 내용은 [CodeMirror 6 문서](https://codemirror.net/docs/)를 참조하세요.

## 편집기 확장이 필요한가요?

편집기 확장을 구축하는 것은 도전적일 수 있으므로, 실제로 그것이 필요한지 고려하세요.

-   읽기 뷰에서 Markdown을 HTML로 변환하는 방식을 변경하려는 경우, [Markdown 후처리기](../../editor/markdown-post-processing.md)를 구축해보세요.
-   라이브 프리뷰에서 문서의 모양과 느낌을 변경하려는 경우, 편집기 확장을 구축해야 합니다.

## 편집기 확장 등록하기

CodeMirror 6 (CM6)은 웹 기술을 사용하여 코드를 편집하기 위한 강력한 엔진입니다. 핵심적으로, 편집기 자체에는 최소한의 기능 세트가 있습니다. 현대적인 편집기에서 기대할 수 있는 모든 기능은 선택하여 사용할 수 있는 *확장(extension)*으로 제공됩니다. Obsidian에는 이러한 확장들이 이미 함께 제공되지만, 직접 등록할 수도 있습니다.

편집기 확장을 등록하려면 Obsidian 플러그인의 `onload` 메서드에서 [registerEditorExtension](../../reference/typescript/classes/Plugin_2.md#registereditorextension)을 사용하세요:

```ts
onload() {
  this.registerEditorExtension([examplePlugin, exampleField]);
}
```

CM6은 여러 유형의 확장(extension)을 지원하지만, 가장 일반적인 유형인 [뷰 플러그인](view-plugins.md)과 [상태 필드](state-fields.md) 중 두 가지입니다.
