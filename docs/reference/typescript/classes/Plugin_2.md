# Plugin_2

Extends `Component`

## Constructor

```ts
constructor(app: App, manifest: PluginManifest);
```

## Properties

### app

```ts
app: App;
```

### manifest

```ts
manifest: PluginManifest;
```

## Methods

### addRibbonIcon

```ts
addRibbonIcon(icon: IconName, title: string, callback: (evt: MouseEvent) => any): HTMLElement;
```

리본 아이콘을 왼쪽 막대에 추가합니다.

### addStatusBarItem

```ts
addStatusBarItem(): HTMLElement;
```

### addCommand

```ts
addCommand(command: Command): Command;
```

명령어를 전역적으로 등록합니다. 명령어 ID와 이름은 자동으로 이 플러그인의 ID와 이름 앞에 붙여집니다.

### addSettingTab

```ts
addSettingTab(settingTab: PluginSettingTab): void;
```

### registerView

```ts
registerView(type: string, viewCreator: ViewCreator): void;
```

### registerHoverLinkSource

```ts
registerHoverLinkSource(id: string, info: HoverLinkSource): void;
```

이벤트의 `Hover-link` 에미터로 `Page preview` 코어 플러그인에 보기를 등록합니다.

### registerExtensions

```ts
registerExtensions(extensions: string[], viewType: string): void;
```

### registerMarkdownPostProcessor

```ts
registerMarkdownPostProcessor(postProcessor: MarkdownPostProcessor, sortOrder?: number): MarkdownPostProcessor;
```

### registerMarkdownCodeBlockProcessor

```ts
registerMarkdownCodeBlockProcessor(language: string, handler: (source: string, el: HTMLElement, ctx: MarkdownPostProcessorContext) => Promise<any> | void, sortOrder?: number): MarkdownPostProcessor;
```

지정된 언어와 핸들러에 울타리가 쳐진 코드를 처리하는 특별한 포스트 프로세서를 등록합니다.
이 특수 포스트 프로세서는 &lt;pre&gt;&lt;code&gt;를 제거하고 다음과 같은 &lt;div&gt;를 생성합니다
처리기로 전달되며 사용자 정의 요소로 채워질 것으로 예상됩니다.

### registerCodeMirror

```ts
registerCodeMirror(callback: (cm: CodeMirror.Editor) => any): void;
```

현재 로드된 모든 CodeMirror 인스턴스에 대해 콜백을 실행합니다,
그런 다음 이후의 모든 CodeMirror 인스턴스에 대한 콜백을 등록합니다.

### registerEditorExtension

```ts
registerEditorExtension(extension: Extension): void;
```

CodeMirror 6 확장자를 등록합니다.
즉시 플러그인을 위해 cm6 확장을 재구성하려면 여기에 배열을 전달하고 동적으로
수정합니다. 이 배열이 수정되면 `Workspace.updateOptions()`를 호출하여 변경 사항을 적용합니다.

### registerObsidianProtocolHandler

```ts
registerObsidianProtocolHandler(action: string, handler: ObsidianProtocolHandler): void;
```

obsidian:// URL에 대한 핸들러를 등록합니다.

### registerEditorSuggest

```ts
registerEditorSuggest(editorSuggest: EditorSuggest<any>): void;
```

사용자가 입력하는 동안 라이브 제안을 제공할 수 있는 EditorSuggest를 등록합니다.

### loadData

```ts
loadData(): Promise<any>;
```

### saveData

```ts
saveData(data: any): Promise<void>;
```
