# Document

브라우저에 로드된 모든 웹 페이지는 DOM 트리인 웹 페이지의 내용에 대한 진입점 역할을 합니다.

## Properties

### \_EVENTS

```ts
_EVENTS: { fullscreenchange?: EventListenerInfo[]; fullscreenerror?: EventListenerInfo[]; pointerlockchange?: EventListenerInfo[]; pointerlockerror?: EventListenerInfo[]; ... 91 more ...; paste?: EventListenerInfo[]; }
```

## Methods

### on

```ts
on: <K extends "input" | "progress" | "select" | "fullscreenchange" | "fullscreenerror" | "abort" | "animationcancel" | "animationend" | "animationiteration" | "animationstart" | "auxclick" | ... 84 more ... | "visibilitychange">(this: Document, type: K, selector: string, listener: (this: Document, ev: DocumentEventMap[...
```

### off

```ts
off: <K extends "input" | "progress" | "select" | "fullscreenchange" | "fullscreenerror" | "abort" | "animationcancel" | "animationend" | "animationiteration" | "animationstart" | "auxclick" | ... 84 more ... | "visibilitychange">(this: Document, type: K, selector: string, listener: (this: Document, ev: DocumentEventMap[...
```
