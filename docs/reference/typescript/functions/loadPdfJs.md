# loadPdfJs

```ts
export function loadPdfJs(): Promise<any>;
```

PDF.js를 로드하고 글로벌 pdfjsLib 개체에 약속을 반환합니다.
이 약속이 동일한 참조를 받기로 결정된 후에 `window.pdfjsLib`을 사용할 수도 있습니다.
