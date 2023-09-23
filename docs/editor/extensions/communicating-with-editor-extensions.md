---
sidebar_position: 40
---

# 편집기 확장과의 통신

편집기 확장을 구축한 후에는 편집기 외부에서 해당 확장과 통신하고자 할 수 있습니다. 예를 들어, [명령어](../../user-interface/commands.md)나 [리본 액션](../../user-interface/ribbon-actions.md)을 통해 가능합니다.

[MarkdownView](../../reference/typescript/classes/MarkdownView.md)에서 CodeMirror 6 편집기에 접근할 수 있습니다. 그러나 Obsidian API는 실제로 편집기를 노출시키지 않으므로 `@ts-expect-error`를 사용하여 TypeScript에 해당 객체가 존재함을 알려야 합니다.

```ts
import { EditorView } from "@codemirror/view";

// @ts-expect-error, not typed
const editorView = view.editor.cm as EditorView;
```

## 뷰 플러그인

[뷰 플러그인](view-plugins.md) 인스턴스에는 `EditorView.plugin()` 메서드를 사용하여 접근할 수 있습니다.

```ts title="main.ts" {8-12}
this.addCommand({
    id: "example-editor-command",
    name: "Example editor command",
    editorCallback: (editor, view) => {
        // @ts-expect-error, not typed
        const editorView = view.editor.cm as EditorView;

        const plugin = editorView.plugin(examplePlugin);

        if (plugin) {
            plugin.addPointerToSelection(editorView);
        }
    },
});
```

## 상태 필드

편집기 뷰에서 변경 사항을 디스패치하고 [상태 효과](state-fields.md#dispatching-state-effects)를 직접 처리할 수 있습니다.

```ts title="main.ts" {8-12}
this.addCommand({
    id: "example-editor-command",
    name: "Example editor command",
    editorCallback: (editor, view) => {
        // @ts-expect-error, not typed
        const editorView = view.editor.cm as EditorView;

        editorView.dispatch({
            effects: [
                // ...
            ],
        });
    },
});
```
