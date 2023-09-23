# loadMermaid

```ts
export function loadMermaid(): Promise<any>;
```

Mermaid를 로드하고 전역 `mermaid` 객체에 대한 프로미스를 반환합니다.
이 프로미스가 해결된 후에도 `mermaid`를 사용하여 동일한 참조를 얻을 수 있습니다.
