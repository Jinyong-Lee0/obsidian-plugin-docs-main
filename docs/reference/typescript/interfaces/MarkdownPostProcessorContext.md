# MarkdownPostProcessorContext

## 속성

### docId

```ts
docId: string;
```

문서의 ID입니다.

### sourcePath

```ts
sourcePath: string;
```

소스 경로입니다.

### frontmatter

```ts
frontmatter: any;
```

프론트매터(frontmatter)입니다.

## 메서드

### addChild

```ts
addChild: (child: MarkdownRenderChild) => void
```

렌더러가 수명 주기를 관리하는 자식 컴포넌트를 추가합니다.

이 함수를 사용하여 종속적인 자식을 렌더러에 추가하면, 자식의 containerEl이 제거되면 컴포넌트의 unload가 호출됩니다.

### getSectionInfo

```ts
getSectionInfo: (el: HTMLElement) => MarkdownSectionInformation;
```

해당 요소의 현재 섹션 정보를 가져옵니다.
가장 최신 버전의 정보를 얻기 위해 이 함수는 필요한 순간에 직접 호출해야 합니다.
이 함수는 많은 경우 null을 반환할 수도 있습니다. 사용할 경우 null 처리에 대비해야 합니다.
