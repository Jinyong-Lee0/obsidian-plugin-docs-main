# FileManager

UI에서 파일 생성, 삭제 및 이름 변경을 관리합니다.

## Constructor

```ts
constructor();
```

## Methods

### getNewFileParent

```ts
getNewFileParent(sourcePath: string): TFolder;
```

사용자의 기본 설정에 따라 새 파일을 저장할 폴더를 가져옵니다.

### renameFile

```ts
renameFile(file: TAbstractFile, newPath: string): Promise<void>;
```

파일 이름을 안전하게 바꾸거나 이동하고, 사용자의 기본 설정에 따라 파일에 대한 모든 링크를 업데이트합니다.

### generateMarkdownLink

```ts
generateMarkdownLink(file: TFile, sourcePath: string, subpath?: string, alias?: string): string;
```

사용자의 기본 설정에 따라 마크다운 링크를 생성합니다.

### processFrontMatter

```ts
processFrontMatter(file: TFile, fn: (frontMatter: any) => void): Promise<void>;
```

노트의 앞부분을 원자적으로 읽고 수정하며 저장합니다.
전면 물질은 JS 객체로 전달되며 원하는 결과를 얻기 위해 직접 변형되어야 합니다.

이 방법으로 발생한 오류를 처리해야 합니다.
