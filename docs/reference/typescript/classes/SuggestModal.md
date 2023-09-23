# SuggestModal

Extends `Modal`

Implements `ISuggestOwner<T>`

## Constructor

```ts
constructor(app: App);
```

## Properties

### limit

```ts
limit: number;
```

### emptyStateText

```ts
emptyStateText: string;
```

### inputEl

```ts
inputEl: HTMLInputElement;
```

### resultContainerEl

```ts
resultContainerEl: HTMLElement;
```

## Methods

### setPlaceholder

```ts
setPlaceholder(placeholder: string): void;
```

### setInstructions

```ts
setInstructions(instructions: Instruction[]): void;
```

### onNoSuggestion

```ts
onNoSuggestion(): void;
```

### selectSuggestion

```ts
selectSuggestion(value: T, evt: MouseEvent | KeyboardEvent): void;
```

사용자가 선택할 때 호출됩니다.

### getSuggestions

```ts
abstract getSuggestions(query: string): T[] | Promise<T[]>;
```

### renderSuggestion

```ts
abstract renderSuggestion(value: T, el: HTMLElement): any;
```

제안 항목을 DOM으로 렌더링합니다.

### onChooseSuggestion

```ts
abstract onChooseSuggestion(item: T, evt: MouseEvent | KeyboardEvent): any;
```
