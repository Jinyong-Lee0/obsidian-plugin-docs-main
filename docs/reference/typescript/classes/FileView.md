# FileView

Extends `ItemView`

## Constructor

```ts
constructor(leaf: WorkspaceLeaf);
```

## Properties

### allowNoFile

```ts
allowNoFile: boolean;
```

### file

```ts
file: TFile;
```

### navigation

```ts
navigation: boolean;
```

보기가 탐색을 위한 것인지 여부입니다.
보기가 탐색할 목적이 아닌 정적 보기인 경우 이를 false로 설정합니다.
(예: 파일 탐색기, 캘린더 등)
보기에서 파일을 열거나 탐색할 수 있는 경우 true로 설정합니다. (예: Markdown Editor view, Kanban view, PDF view 등)
파일 보기는 기본적으로 탐색할 수 있습니다.

## Methods

### getDisplayText

```ts
getDisplayText(): string;
```

### onload

```ts
onload(): void;
```

구성 요소를 로드하려면 이 값을 재정의하십시오

### getState

```ts
getState(): any;
```

### setState

```ts
setState(state: any, result: ViewStateResult): Promise<void>;
```

### onLoadFile

```ts
onLoadFile(file: TFile): Promise<void>;
```

### onUnloadFile

```ts
onUnloadFile(file: TFile): Promise<void>;
```

### onRename

```ts
onRename(file: TFile): Promise<void>;
```

### canAcceptExtension

```ts
canAcceptExtension(extension: string): boolean;
```
