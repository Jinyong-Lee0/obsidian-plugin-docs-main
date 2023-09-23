# PopoverSuggest

Implements `ISuggestOwner<T>`, `CloseableComponent`

## Constructor

```ts
constructor(app: App, scope: Scope);
```

## Methods

### open

```ts
open(): void;
```

### close

```ts
close(): void;
```

### renderSuggestion

```ts
abstract renderSuggestion(value: T, el: HTMLElement): void;
```

제안 항목을 DOM으로 렌더링합니다.

### selectSuggestion

```ts
abstract selectSuggestion(value: T, evt: MouseEvent | KeyboardEvent): void;
```

사용자가 선택할 때 호출됩니다.
