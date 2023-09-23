# iterateCacheRefs

```ts
export function iterateCacheRefs(
    cache: CachedMetadata,
    cb: (ref: ReferenceCache) => boolean | void
): boolean;
```

링크와 임베드를 반복합니다. 콜백 함수가 true를 반환하면 반복 프로세스가 중단됩니다.

## Parameters

| Parameter | Description |
| --------- | ----------- |
| `cache`   |             |
| `cb`      |             |
