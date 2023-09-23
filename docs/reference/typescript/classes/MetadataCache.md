# MetadataCache

Extends `Events`

링크 텍스트는 "My note#Heading"과 같이 경로와 하위 경로로 구성된 내부 링크입니다
링크 경로(또는 경로)는 링크 텍스트의 경로 부분입니다
하위 경로는 링크 텍스트의 머리글/블록 ID 부분입니다.

## Constructor

```ts
constructor();
```

## Properties

### resolvedLinks

```ts
resolvedLinks: Record<string, Record<string, number>>;
```

확인된 모든 링크를 포함합니다. 이 개체는 각 소스 파일의 경로를 링크 개수가 있는 대상 파일 경로의 개체에 매핑합니다.
소스 및 대상 경로는 모두 `TFile.path`에서 가져온 볼트 절대 경로이며 `Vault.getAbstractFileByPath(path)`와 함께 사용할 수 있습니다.

### unresolvedLinks

```ts
unresolvedLinks: Record<string, Record<string, number>>;
```

확인되지 않은 모든 링크를 포함합니다. 이 개체는 각 소스 파일을 카운트가 있는 알 수 없는 대상의 개체에 매핑합니다.
소스 경로는 `resolved Links`와 유사한 모든 볼트 절대 경로입니다.

## Methods

### getFirstLinkpathDest

```ts
getFirstLinkpathDest(linkpath: string, sourcePath: string): TFile | null;
```

링크 경로에 가장 적합한 항목을 가져옵니다.

### getFileCache

```ts
getFileCache(file: TFile): CachedMetadata | null;
```

### getCache

```ts
getCache(path: string): CachedMetadata | null;
```

### fileToLinktext

```ts
fileToLinktext(file: TFile, sourcePath: string, omitMdExtension?: boolean): string;
```

파일에 대한 링크 텍스트를 생성합니다.

파일 이름이 고유한 경우 파일 이름을 사용합니다.
고유하지 않은 경우 전체 경로를 사용합니다.

### on

```ts
on(name: 'changed', callback: (file: TFile, data: string, cache: CachedMetadata) => any, ctx?: any): EventRef;
```

파일이 색인화되고 이제 해당(업데이트된) 캐시를 사용할 수 있게 되면 호출됩니다.

참고: 성능상의 이유로 파일 이름이 변경된 경우에는 호출되지 않습니다.
볼트 이름 변경 이벤트를 후크해야 합니다.
(상세정보 : https://github.com/obsidianmd/obsidian-api/issues/77)
파일이 삭제되면 호출됩니다. 캐시된 메타데이터의 Best-Effort 이전 버전이 표시됩니다,
파일이 이전에 캐시되지 않은 경우 null일 수 있습니다.
`resolved Links` 및 `resolved Links`에 대한 파일이 확인되면 호출됩니다.
파일이 색인화된 후에 이 문제가 발생하는 경우가 있습니다.
모든 파일이 해결되면 호출되며, 처음 로드 후 파일이 수정될 때마다 실행됩니다.

### on

```ts
on(name: 'deleted', callback: (file: TFile, prevCache: CachedMetadata | null) => any, ctx?: any): EventRef;
```

파일이 색인화되고 이제 해당(업데이트된) 캐시를 사용할 수 있게 되면 호출됩니다.

참고: 성능상의 이유로 파일 이름이 변경된 경우에는 호출되지 않습니다.
볼트 이름 변경 이벤트를 후크해야 합니다.
(상세정보 : https://github.com/obsidianmd/obsidian-api/issues/77)
파일이 삭제되면 호출됩니다. 캐시된 메타데이터의 Best-Effort 이전 버전이 표시됩니다,
파일이 이전에 캐시되지 않은 경우 null일 수 있습니다.
`resolved Links` 및 `resolved Links`에 대한 파일이 확인되면 호출됩니다.
파일이 색인화된 후에 이 문제가 발생하는 경우가 있습니다.
모든 파일이 해결되면 호출되며, 처음 로드 후 파일이 수정될 때마다 실행됩니다.

### on

```ts
on(name: 'resolve', callback: (file: TFile) => any, ctx?: any): EventRef;
```

파일이 색인화되고 이제 해당(업데이트된) 캐시를 사용할 수 있게 되면 호출됩니다.

참고: 성능상의 이유로 파일 이름이 변경된 경우에는 호출되지 않습니다.
볼트 이름 변경 이벤트를 후크해야 합니다.
(상세정보 : https://github.com/obsidianmd/obsidian-api/issues/77)
파일이 삭제되면 호출됩니다. 캐시된 메타데이터의 Best-Effort 이전 버전이 표시됩니다,
파일이 이전에 캐시되지 않은 경우 null일 수 있습니다.
`resolved Links` 및 `resolved Links`에 대한 파일이 확인되면 호출됩니다.
파일이 색인화된 후에 이 문제가 발생하는 경우가 있습니다.
모든 파일이 해결되면 호출되며, 처음 로드 후 파일이 수정될 때마다 실행됩니다.

### on

```ts
on(name: 'resolved', callback: () => any, ctx?: any): EventRef;
```

파일이 색인화되고 이제 해당(업데이트된) 캐시를 사용할 수 있게 되면 호출됩니다.

참고: 성능상의 이유로 파일 이름이 변경된 경우에는 호출되지 않습니다.
볼트 이름 변경 이벤트를 후크해야 합니다.
(상세정보 : https://github.com/obsidianmd/obsidian-api/issues/77)
파일이 삭제되면 호출됩니다. 캐시된 메타데이터의 Best-Effort 이전 버전이 표시됩니다,
파일이 이전에 캐시되지 않은 경우 null일 수 있습니다.
`resolved Links` 및 `resolved Links`에 대한 파일이 확인되면 호출됩니다.
파일이 색인화된 후에 이 문제가 발생하는 경우가 있습니다.
모든 파일이 해결되면 호출되며, 처음 로드 후 파일이 수정될 때마다 실행됩니다.
