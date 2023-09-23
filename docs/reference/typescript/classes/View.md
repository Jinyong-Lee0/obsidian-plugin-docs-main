# View

Extends `Component`

## Constructor

```ts
constructor(leaf: WorkspaceLeaf);
```

## Properties

### app

```ts
app: App;
```

### icon

```ts
icon: string;
```

### navigation

```ts
navigation: boolean;
```

뷰가 네비게이션을 위한 것인지 여부를 나타냅니다.
뷰가 정적이며 탐색할 의도가 없다면 이 값을 false로 설정합니다.
(예: 파일 탐색기, 캘린더 등)
뷰에서 파일을 열거나 다른 방식으로 탐색할 수 있다면 이 값을 true로 설정합니다.
(예: 마크다운 에디터 뷰, 칸반 뷰, PDF 뷰 등)

### leaf

```ts
leaf: WorkspaceLeaf;
```

### containerEl

```ts
containerEl: HTMLElement;
```

## Methods

### onOpen

```ts
protected onOpen(): Promise<void>;
```

### onClose

```ts
protected onClose(): Promise<void>;
```

### getViewType

```ts
abstract getViewType(): string;
```

### getState

```ts
getState(): any;
```

### setState

```ts
setState(state: any, result: ViewStateResult): Promise<void>;
```

### getEphemeralState

```ts
getEphemeralState(): any;
```

### setEphemeralState

```ts
setEphemeralState(state: any): void;
```

### getIcon

```ts
getIcon(): IconName;
```

### onResize

```ts
onResize(): void;
```

이 뷰의 크기가 변경될 때 호출됩니다.

### getDisplayText

```ts
abstract getDisplayText(): string;
```

### onPaneMenu

```ts
onPaneMenu(menu: Menu, source: 'more-options' | 'tab-header' | string): void;
```

패널 메뉴를 채웁니다.

(이전에 제거된 `onHeaderMenu`와 `onMoreOptionsMenu`를 대체합니다)
