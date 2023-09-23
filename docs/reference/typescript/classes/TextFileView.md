# TextFileView

Extends `EditableFileView`

이 클래스는 일반 텍스트 기반 편집 가능한 파일 보기를 구현하며, 이는 주어진 편집기를 로드하고 저장할 수 있습니다.

기본적으로 이 보기는 닫힐 때만 저장됩니다. 자동 저장을 구현하려면 편집자가
내용이 변경되면 `this.requestSave()`를 호출합니다.

## Constructor

```ts
constructor(leaf: WorkspaceLeaf);
```

## Properties

### data

```ts
data: string;
```

In memory data

### requestSave

```ts
requestSave: () => void
```

지금부터 2초 후 저장 취소

## Methods

### onUnloadFile

```ts
onUnloadFile(file: TFile): Promise<void>;
```

### onLoadFile

```ts
onLoadFile(file: TFile): Promise<void>;
```

### save

```ts
save(clear?: boolean): Promise<void>;
```

### getViewData

```ts
abstract getViewData(): string;
```

편집기에서 데이터를 가져옵니다. 편집기 내용을 파일에 저장하기 위해 호출됩니다.

### setViewData

```ts
abstract setViewData(data: string, clear: boolean): void;
```

편집기에 데이터를 설정합니다. 파일 내용을 로드하는 데 사용됩니다.

clear가 설정되어 있으면 완전히 다른 파일을 여는 것을 의미합니다. 그런 경우 clear()를 호출하거나 새로운 데이터를 설정할 때 조금 더 효율적인 clearing 메커니즘을 구현해야 합니다.

### clear

```ts
abstract clear(): void;
```

편집기 지우기. 보통 완전히 다른 파일을 열려고 할 때 호출되므로 실행 취소 기록과 같은 편집기 상태 및 이전 파일 내용과 관련된 캐시/인덱스를 지우는 것이 좋습니다.
