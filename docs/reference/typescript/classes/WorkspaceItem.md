# WorkspaceItem

`Events`를 확장합니다.

## Constructor

```ts
constructor();
```

## Methods

### getRoot

```ts
getRoot(): WorkspaceItem;
```

### getContainer

```ts
getContainer(): WorkspaceContainer;
```

루트 컨테이너 부모 항목을 가져옵니다. 가능한 값은 다음 중 하나입니다:

-   {@link WorkspaceRoot}
-   {@link WorkspaceWindow}
