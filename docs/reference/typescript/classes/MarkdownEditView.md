# MarkdownEditView

Implements `MarkdownSubView`, `HoverParent`, `MarkdownFileInfo`

옵시디언 모바일의 편집자이자 곧 출시될 WYSIWYG 편집자입니다.

## Constructor

```ts
constructor(view: MarkdownView);
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

### clear

```ts
clear(): void;
```

### get

```ts
get(): string;
```

### set

```ts
set(data: string, clear: boolean): void;
```

### getSelection

```ts
getSelection(): string;
```

### getScroll

```ts
getScroll(): number;
```

### applyScroll

```ts
applyScroll(scroll: number): void;
```
