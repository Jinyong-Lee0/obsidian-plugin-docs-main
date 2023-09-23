# Node

Node는 DOM API 객체 유형이 상속하는 인터페이스입니다. 이를 통해 해당 유형을 동일하게 처리하거나 동일한 방식으로 테스트할 수 있습니다.

## 메서드

### createEl

```ts
createEl: <K extends "object" | "a" | "abbr" | "address" | "applet" | "area" | "article" | "aside" | "audio" | "b" | ... 99 more ... | "wbr">(tag: K, o?: string | DomElementInfo, callback?: (el: HTMLElementTagNameMap[K]) => void) => HTM...
```

요소를 생성하고 이 노드에 추가합니다.

### createDiv

```ts
createDiv: (
    o?: string | DomElementInfo,
    callback?: (el: HTMLDivElement) => void
) => HTMLDivElement;
```

div 요소를 생성하고 반환합니다.

### createSpan

```ts
createSpan: (
    o?: string | DomElementInfo,
    callback?: (el: HTMLSpanElement) => void
) => HTMLSpanElement;
```

span 요소를 생성하고 반환합니다.

### createSvg

```ts
createSvg: <K extends "symbol" | "a" | "script" | "style" | "title" | "circle" | "clipPath" | "defs" | "desc" | "ellipse" | "feBlend" | "feColorMatrix" | "feComponentTransfer" | "feComposite" | "feConvolveMatrix" | ... 41 more ... | "view">(tag: K, o?: string | SvgElementInfo, callback?: (el: SVGElementTagNameMap[K]) => void) ...
```
