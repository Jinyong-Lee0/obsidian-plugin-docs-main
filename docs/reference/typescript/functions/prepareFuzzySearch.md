# prepareFuzzySearch

```ts
export function prepareFuzzySearch(
    query: string
): (text: string) => SearchResult | null;
```

대상 문자열에서 실행되는 퍼지 검색 콜백을 구성합니다.
검색을 몇 천 번 이상 실행하는 경우 성능 문제가 발생할 수 있습니다.
성능에 문제가 있는 경우 `prepare Simple Search`를 사용하는 것을 고려해 보십시오.

## Parameters

| Parameter | Description      |
| --------- | ---------------- |
| `query`   | the fuzzy query. |
