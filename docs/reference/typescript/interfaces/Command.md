# Command

## 속성

### id

```ts
id: string;
```

이 명령을 식별하는 전역적으로 고유한 ID입니다.

### name

```ts
name: string;
```

검색을 위한 사용자 친화적인 이름입니다.

### icon

```ts
icon: string;
```

툴바에 사용할 아이콘 ID입니다.

### mobileOnly

```ts
mobileOnly: boolean;
```

모바일에서만 사용 가능한지 여부입니다.

### repeatable

```ts
repeatable: boolean;
```

핫키를 계속 누르고 있으면 이 명령이 반복해서 트리거되어야 하는지 여부입니다. 기본값은 false입니다.

### callback

```ts
callback: () => any;
```

간단한 콜백으로, 전역적으로 트리거됩니다.

### checkCallback

```ts
checkCallback: (checking: boolean) => boolean | void
```

복잡한 콜백으로, 간단한 콜백을 재정의합니다.
현재 상황에서 해당 명령을 수행할 수 있는지 "확인"하는 데 사용됩니다.
예를 들어, 명령이 활성화된 포커스된 패인이 MarkdownSourceView여야 하는 경우,
해당 조건이 충족되면 true만 반환해야 합니다. false나 undefined를 반환하면,
명령은 명령 팔레트에서 숨겨집니다.

### editorCallback

```ts
editorCallback: (editor: Editor, ctx: MarkdownView | MarkdownFileInfo) => any;
```

사용자가 편집기에 있는 경우에만 트리거되는 명령 콜백입니다.
`callback` 및 `checkCallback`을 재정의합니다.

### editorCheckCallback

```ts
editorCheckCallback:(checking:boolean , editor :Editor , ctx :MarkdownView|MarkdownFileInfo)=>boolean|void
```

사용자가 편집기에 있는 경우에만 트리거되는 명령 콜백 입니다.
`editorCallback`, `callback`, 그리고 `checkCallbakc` 을 재정의 합니다.

### hotkeys

```ts
hotkeys : Hotkey[]
```

디폴트 핫키를 설정합니다. 가능하다면 디폴트 핫키 설정은 피하는 것이 좋습니다.
사용자가 설정한 핫키와 충돌하지 않도록 하기 위함 입니다. 단 맞춤형 핫크는 더 높은 우선순위를 가지게 됩니다
