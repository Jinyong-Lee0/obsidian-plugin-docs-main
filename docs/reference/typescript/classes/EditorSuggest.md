# EditorSuggest

Extends `PopoverSuggest<T>`

## Constructor

```ts
constructor(app: App);
```

## Properties

### context

```ts
context: EditorSuggestContext;
```

`on Trigger`의 결과를 포함하는 현재 제안 컨텍스트.
EditorSuggest가 실행되지 않아야 할 때마다 null이 됩니다.

### limit

```ts
limit: number;
```

제안 항목에 다른 제한을 사용하려면 이 값을 재정의합니다

## Methods

### setInstructions

```ts
setInstructions(instructions: Instruction[]): void;
```

### onTrigger

```ts
abstract onTrigger(cursor: EditorPosition, editor: Editor, file: TFile): EditorSuggestTriggerInfo | null;
```

편집기 선과 커서 위치를 기준으로 이 Editor Suggest(편집기 제안)를 지금 트리거해야 하는지 여부를 결정합니다.
일반적으로 커서 앞에 있는 현재 줄 텍스트에 정규식을 실행합니다.
null을 반환하여 이 편집자 제안이 트리거되지 않아야 함을 나타냅니다.

이 기능은 (각 키 누름에서) 매우 자주 트리거되므로 성능에 유의해야 합니다.
단순하게 유지하고, 적절한 시기가 아니라고 판단되면 가능한 한 빨리 null을 반환합니다.

### getSuggestions

```ts
abstract getSuggestions(context: EditorSuggestContext): T[] | Promise<T[]>;
```

이 컨텍스트를 기반으로 제안 항목을 생성합니다. 비동기식일 수 있지만 가급적이면 동기화할 수 있습니다.
비동기 제안을 생성할 때는 컨텍스트를 전달해야 합니다.
