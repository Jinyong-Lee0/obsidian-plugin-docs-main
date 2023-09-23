# debounce

```ts
export function debounce<T extends unknown[], V>(
    cb: (...args: [...T]) => V,
    timeout?: number,
    resetTimer?: boolean
): Debouncer<T, V>;
```

표준 디바운스 함수입니다.

## 매개변수

| 매개변수     | 설명                                                        |
| ------------ | ----------------------------------------------------------- |
| `cb`         | 호출할 함수입니다.                                          |
| `timeout`    | 대기할 시간 초과입니다.                                     |
| `resetTimer` | 디바운서가 다시 호출될 때 타임아웃을 재설정할지 여부입니다. |
