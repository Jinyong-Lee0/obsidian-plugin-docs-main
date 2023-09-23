# prepareSimpleSearch

```ts
export function prepareSimpleSearch(
    query: string
): (text: string) => SearchResult | null;
```

대상 문자열에서 실행되는 간단한 검색 콜백을 구성합니다.

## Parameters

| Parameter | Description               |
| --------- | ------------------------- |
| `query`   | the space-separated words |
