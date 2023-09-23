# Component

## Constructor

```ts
constructor();
```

## Methods

### load

```ts
load(): void;
```

이 구성 요소 및 해당 자식 로드

### onload

```ts
onload(): void;
```

구성 요소를 로드하려면 이 값을 재정의하십시오

### unload

```ts
unload(): void;
```

이 구성 요소와 해당 자식을 언로드합니다

### onunload

```ts
onunload(): void;
```

이 값을 재정의하여 구성 요소를 언로드합니다

### addChild

```ts
addChild<T extends Component>(component: T): T;
```

자식 구성 요소를 추가하고, 이 구성 요소가 로드된 경우 로드합니다

### removeChild

```ts
removeChild<T extends Component>(component: T): T;
```

하위 구성요소를 제거하고, 이를 언로딩합니다

### register

```ts
register(cb: () => any): void;
```

언로딩 시 호출할 콜백을 등록합니다

### registerEvent

```ts
registerEvent(eventRef: EventRef): void;
```

언로딩 시 분리될 이벤트를 등록합니다

### registerDomEvent

```ts
registerDomEvent<K extends keyof WindowEventMap>(el: Window, type: K, callback: (this: HTMLElement, ev: WindowEventMap[K]) => any, options?: boolean | AddEventListenerOptions): void;
```

언로딩 시 분리할 DOM 이벤트를 등록합니다

### registerDomEvent

```ts
registerDomEvent<K extends keyof DocumentEventMap>(el: Document, type: K, callback: (this: HTMLElement, ev: DocumentEventMap[K]) => any, options?: boolean | AddEventListenerOptions): void;
```

언로딩 시 분리할 DOM 이벤트를 등록합니다

### registerDomEvent

```ts
registerDomEvent<K extends keyof HTMLElementEventMap>(el: HTMLElement, type: K, callback: (this: HTMLElement, ev: HTMLElementEventMap[K]) => any, options?: boolean | AddEventListenerOptions): void;
```

언로딩 시 분리할 DOM 이벤트를 등록합니다

### registerScopeEvent

```ts
registerScopeEvent(keyHandler: KeymapEventHandler): void;
```

언로딩 시 분리할 주요 이벤트를 등록합니다

### registerInterval

```ts
registerInterval(id: number): number;
```

언로딩 시 취소할 간격(setInterval에서)을 등록합니다
NodeJS와 브라우저 API 간에 TypeScript가 혼동되지 않도록 하려면 {@linksetInterval} 대신 {@linkwindow.setInterval}을(를) 사용하십시오
