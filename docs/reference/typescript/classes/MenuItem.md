# MenuItem

## Constructor

```ts
constructor();
```

## Methods

### setTitle

```ts
setTitle(title: string | DocumentFragment): this;
```

### setIcon

```ts
setIcon(icon: IconName | null): this;
```

### setChecked

```ts
setChecked(checked: boolean | null): this;
```

### setDisabled

```ts
setDisabled(disabled: boolean): this;
```

### setIsLabel

```ts
setIsLabel(isLabel: boolean): this;
```

### onClick

```ts
onClick(callback: (evt: MouseEvent | KeyboardEvent) => any): this;
```

### setSection

```ts
setSection(section: string): this;
```

이 메뉴 항목이 속해야 할 섹션을 설정합니다.
기존 메뉴의 섹션 ID를 찾으려면 DOM 요소를 검사합니다
`데이터 섹션` 속성을 확인합니다.
