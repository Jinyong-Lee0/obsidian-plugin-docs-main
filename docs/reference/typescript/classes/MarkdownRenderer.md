# MarkdownRenderer

Extends `MarkdownRenderChild`

Implements `MarkdownPreviewEvents`, `HoverParent`

## Constructor

```ts
constructor(containerEl: HTMLElement);
```

## Properties

### app

```ts
app: App;
```

### hoverPopover

```ts
hoverPopover: HoverPopover;
```

## Methods

### renderMarkdown

```ts
static renderMarkdown(markdown: string, el: HTMLElement, sourcePath: string, component: Component): Promise<void>;
```

HTML 요소에 마크다운 문자열을 렌더링합니다.
