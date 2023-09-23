# HTMLElement

HTML 요소입니다. 일부 요소는 직접 이 인터페이스를 구현하고, 다른 요소는 이를 상속하는 인터페이스를 통해 구현합니다.

## Properties

### \_EVENTS

```ts
_EVENTS: { fullscreenchange?: EventListenerInfo[]; fullscreenerror?: EventListenerInfo[]; abort?: EventListenerInfo[]; animationcancel?: EventListenerInfo[]; ... 87 more ...; paste?: EventListenerInfo[]; }
```

## Methods

### on

```ts
on: <K extends "input" | "progress" | "select" | "fullscreenchange" | "fullscreenerror" | "abort" | "animationcancel" | "animationend" | "animationiteration" | "animationstart" | "auxclick" | ... 80 more ... | "paste">(this: HTMLElement, type: K, selector: string, listener: (this: HTMLElement, ev: HTMLElementEventMap[K]...
```

### off

```ts
off: <K extends "input" | "progress" | "select" | "fullscreenchange" | "fullscreenerror" | "abort" | "animationcancel" | "animationend" | "animationiteration" | "animationstart" | "auxclick" | ... 80 more ... | "paste">(this: HTMLElement, type: K, selector: string, listener: (this: HTMLElement, ev: HTMLElementEventMap[K]...
```

### onClickEvent

```ts
onClickEvent: (this: HTMLElement, listener: (this: HTMLElement, ev: MouseEvent) => any, options?: boolean | AddEventListenerOptions) => void
```

### onNodeInserted

```ts
onNodeInserted: (this: HTMLElement, listener: () => any, once?: boolean) => () => void
```

### onWindowMigrated

```ts
onWindowMigrated: (this: HTMLElement, listener: (win: Window) => any) => () => void
```

### trigger

```ts
trigger: (eventType: string) => void
```
