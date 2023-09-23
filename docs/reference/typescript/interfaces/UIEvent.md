# UIEvent

간단한 사용자 인터페이스 이벤트입니다.

## 속성

### targetNode

```ts
targetNode: Node;
```

### win

```ts
win: Window;
```

### doc

```ts
doc: Document;
```

## 메서드

### instanceOf

```ts
instanceOf: <T>(type: new (...data: any[]) => T) => this is T
```

UIEvent에 대한 instanceof 체크를 지원하는, UIEvents의 instanceof 체크를 대체할 수 있는 메서드입니다. 다른 창에서도 작동합니다.
