# DocumentFragment

부모가 없는 최소한의 문서 객체입니다. Document의 경량 버전으로, 표준 문서와 마찬가지로 노드로 구성된 문서 구조의 일부를 저장하는 데 사용됩니다. 주요 차이점은 문서 프래그먼트가 활성 문서 트리 구조의 일부가 아니기 때문에 프래그먼트에 대한 변경 사항이 문서에 영향을 주지 않고, 리플로우를 발생시키지 않으며 변경 사항이 발생할 때 발생할 수 있는 성능 영향도 없다는 것입니다.

## 메서드

### find

```ts
find: (selector: string) => HTMLElement;
```

주어진 선택자와 일치하는 첫 번째 HTMLElement를 반환합니다.

### findAll

```ts
findAll: (selector: string) => HTMLElement[]
```

주어진 선택자와 일치하는 모든 HTMLElement를 배열로 반환합니다.
