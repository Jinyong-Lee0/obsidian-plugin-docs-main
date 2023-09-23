# ListItemCache

## 속성

### id

```ts
id: string;
```

이 리스트 항목의 블록 ID입니다.

### task

```ts
task: string;
```

작업의 체크 상태를 나타내는 단일 문자입니다.
공백 문자 `' '`은 미완료된 작업으로 해석됩니다.
다른 문자는 완료된 작업으로 해석됩니다.
이 항목이 작업이 아닌 경우 `undefined`입니다.

### parent

```ts
parent: number;
```

부모 리스트 항목의 줄 번호(position.start.line)입니다.
만약 이 항목에 부모가 없다면(예: 최상위 수준의 리스트인 경우),
이 값은 첫 번째 리스트 항목의 줄 번호에 음수를 취한 값입니다.

동일한 그룹에 속하는 리스트 항목을 추론하는 데 사용할 수 있습니다 (item1.parent === item2.parent).
계층 정보를 재구성하는 데 사용할 수 있습니다 (parentItem.position.start.line === childItem.parent).
