# Keymap

## Constructor

```ts
constructor();
```

## Methods

### pushScope

```ts
pushScope(scope: Scope): void;
```

### popScope

```ts
popScope(scope: Scope): void;
```

### isModifier

```ts
static isModifier(evt: MouseEvent | TouchEvent | KeyboardEvent, modifier: Modifier): boolean;
```

이 이벤트 중에 수정자 키가 눌렸는지 확인합니다

### isModEvent

```ts
static isModEvent(evt?: UserEvent | null): PaneType | boolean;
```

이벤트를 열려야 하는 창 유형으로 변환합니다.
수정자 키 Cmd/Ctrl을 누른 경우 'tab'을 반환하거나 마우스 이벤트를 중간 클릭한 경우 'tab'을 반환합니다.
Cmd/Ctrl+Alt를 누르면 'split'을 반환합니다.
Cmd/Ctrl+Alt+Shift를 누르면 'window'를 반환합니다.
