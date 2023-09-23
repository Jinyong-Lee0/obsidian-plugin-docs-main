# ColorComponent

Extends `ValueComponent<string>`

색상 선택기 구성 요소. 값은 기본적으로 `#000000`과 같은 6자리 해시 접두사가 붙은 16진수 문자열입니다.

## Constructor

```ts
constructor(containerEl: HTMLElement);
```

## Methods

### getValue

```ts
getValue(): HexString;
```

### getValueRgb

```ts
getValueRgb(): RGB;
```

### getValueHsl

```ts
getValueHsl(): HSL;
```

### setValue

```ts
setValue(value: HexString): this;
```

### setValueRgb

```ts
setValueRgb(rgb: RGB): this;
```

### setValueHsl

```ts
setValueHsl(hsl: HSL): this;
```

### onChange

```ts
onChange(callback: (value: string) => any): this;
```
