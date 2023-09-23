# Element

Element는 문서의 모든 객체가 상속하는 가장 일반적인 기본 클래스입니다. 이 클래스에는 모든 종류의 요소에 공통적인 메서드와 속성만 포함되어 있습니다. 더 구체적인 클래스들은 Element를 상속합니다.

## Methods

### find

```ts
find: (selector: string) => Element;
```

### findAll

```ts
findAll: (selector: string) => HTMLElement[]
```

### findAllSelf

```ts
findAllSelf: (selector: string) => HTMLElement[]
```
