# KeymapEventListener

```ts
export type KeymapEventListener = (
    evt: KeyboardEvent,
    ctx: KeymapContext
) => false | any;
```

`false`를 반환하면 자동으로 `preventDefault`가 실행됩니다.
