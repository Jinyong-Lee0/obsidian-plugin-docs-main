# MarkdownView

Extends `TextFileView`

Implements `MarkdownFileInfo`

## Constructor

```ts
constructor(leaf: WorkspaceLeaf);
```

## Properties

### editor

```ts
editor: Editor;
```

### previewMode

```ts
previewMode: MarkdownPreviewView;
```

### currentMode

```ts
currentMode: MarkdownSubView;
```

### hoverPopover

```ts
hoverPopover: HoverPopover;
```

## Methods

### getViewType

```ts
getViewType(): string;
```

### getMode

```ts
getMode(): MarkdownViewModeType;
```

### getViewData

```ts
getViewData(): string;
```

편집기에서 데이터를 가져옵니다. 편집기 내용을 파일에 저장하기 위해 호출됩니다.

### clear

```ts
clear(): void;
```

편집기 지우기. 보통 완전히 다른 파일을 열려고 할 때 호출되므로 실행 취소 기록과 같은 편집기 상태 및 이전 파일 내용과 관련된 캐시/인덱스를 지우는 것이 좋습니다.

### setViewData

```ts
setViewData(data: string, clear: boolean): void;
```

편집기에 데이터를 설정합니다. 파일 내용을 로드하는 데 사용됩니다.

clear가 설정되어 있으면 완전히 다른 파일을 여는 것입니다.
이 경우에는 clear()를 호출하거나 새 데이터를 설정할 경우 좀 더 효율적인 삭제 메커니즘을 구현해야 합니다.

### showSearch

```ts
showSearch(replace?: boolean): void;
```
