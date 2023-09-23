# String

텍스트 문자열의 조작, 형식 지정 및 문자열 내에서 하위 문자열의 결정과 위치를 확인할 수 있습니다.

## 메서드

### contains

```ts
contains: (target: string) => boolean;
```

주어진 대상 문자열이 포함되어 있는지 여부를 반환합니다.

### startsWith

```ts
startsWith: { (searchString: string, position?: number): boolean; (searchString: string, position?: number): boolean; }
```

이 객체의 해당 요소들을 문자열로 변환한 것과 searchString의 해당 요소들이 position에서 시작하는지 여부를 반환합니다. 일치하면 true를 반환하고, 그렇지 않으면 false를 반환합니다.

### endsWith

```ts
endsWith: { (searchString: string, endPosition?: number): boolean; (target: string, length?: number): boolean; }
```

이 객체의 해당 요소들을 문자열로 변환한 것과 searchString의 해당 요소들이 endPosition - length(this)에서 시작하는지 여부를 반환합니다. 일치하면 true를 반환하고, 그렇지 않으면 false를 반환합니다.

### format

```ts
format: (...args: string[]) => string;
```

문자열 내에 지정된 형식으로 인수 값을 삽입하여 형식화된 문자열을 생성합니다.
