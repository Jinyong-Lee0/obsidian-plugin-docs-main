# Menu

Extends `Component`

Implements `CloseableComponent`

## Constructor

```ts
constructor();
```

## Methods

### setNoIcon

```ts
setNoIcon(): this;
```

### setUseNativeMenu

```ts
setUseNativeMenu(useNativeMenu: boolean): this;
```

native 또는 DOM을 사용하려면 이 메뉴를 강제로 사용합니다.
(데스크탑 앱에서만 작동)

### addItem

```ts
addItem(cb: (item: MenuItem) => any): this;
```

메뉴 항목을 추가합니다. 아직 메뉴가 표시되지 않은 경우에만 작동합니다.

### addSeparator

```ts
addSeparator(): this;
```

구분자를 추가합니다. 메뉴가 아직 표시되지 않은 경우에만 작동합니다.

### showAtMouseEvent

```ts
showAtMouseEvent(evt: MouseEvent): this;
```

### showAtPosition

```ts
showAtPosition(position: MenuPositionDef, doc?: Document): this;
```

### hide

```ts
hide(): this;
```

### close

```ts
close(): void;
```

### onHide

```ts
onHide(callback: () => any): void;
```
