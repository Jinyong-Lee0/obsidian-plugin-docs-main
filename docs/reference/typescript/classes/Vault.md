# Vault

Extends `Events`

## Constructor

```ts
constructor();
```

## Properties

### adapter

```ts
adapter: DataAdapter;
```

### configDir

```ts
configDir: string;
```

설정 폴더의 경로를 가져옵니다.
이 값은 일반적으로 `.obsidian`이지만 다를 수 있습니다.

## Methods

### getName

```ts
getName(): string;
```

vault의 이름을 가져옵니다.

### getAbstractFileByPath

```ts
getAbstractFileByPath(path: string): TAbstractFile | null;
```

### getRoot

```ts
getRoot(): TFolder;
```

### create

```ts
create(path: string, data: string, options?: DataWriteOptions): Promise<TFile>;
```

### createBinary

```ts
createBinary(path: string, data: ArrayBuffer, options?: DataWriteOptions): Promise<TFile>;
```

### createFolder

```ts
createFolder(path: string): Promise<void>;
```

### read

```ts
read(file: TFile): Promise<string>;
```

### cachedRead

```ts
cachedRead(file: TFile): Promise<string>;
```

### readBinary

```ts
readBinary(file: TFile): Promise<ArrayBuffer>;
```

### getResourcePath

```ts
getResourcePath(file: TFile): string;
```

### delete

```ts
delete(file: TAbstractFile, force?: boolean): Promise<void>;
```

### trash

```ts
trash(file: TAbstractFile, system: boolean): Promise<void>;
```

시스템 휴지통으로 이동을 시도합니다. 만약 그것이 성공하지 않거나 허용되지 않는다면, 로컬 휴지통을 사용합니다.

### rename

```ts
rename(file: TAbstractFile, newPath: string): Promise<void>;
```

### modify

```ts
modify(file: TFile, data: string, options?: DataWriteOptions): Promise<void>;
```

### modifyBinary

```ts
modifyBinary(file: TFile, data: ArrayBuffer, options?: DataWriteOptions): Promise<void>;
```

### append

```ts
append(file: TFile, data: string, options?: DataWriteOptions): Promise<void>;
```

### process

```ts
process(file: TFile, fn: (data: string) => string, options?: DataWriteOptions): Promise<string>;
```

노트의 내용을 원자적으로 읽고, 수정하고, 저장합니다.

### copy

```ts
copy(file: TFile, newPath: string): Promise<TFile>;
```

### getAllLoadedFiles

```ts
getAllLoadedFiles(): TAbstractFile[];
```

### recurseChildren

```ts
static recurseChildren(root: TFolder, cb: (file: TAbstractFile) => any): void;
```

### getMarkdownFiles

```ts
getMarkdownFiles(): TFile[];
```

### getFiles

```ts
getFiles(): TFile[];
```

### on

```ts
on(name: 'create', callback: (file: TAbstractFile) => any, ctx?: any): EventRef;
```

### on

```ts
on(name: 'modify', callback: (file: TAbstractFile) => any, ctx?: any): EventRef;
```

### on

```ts
on(name: 'delete', callback: (file: TAbstractFile) => any, ctx?: any): EventRef;
```

### on

```ts
on(name: 'rename', callback: (file: TAbstractFile, oldPath: string) => any, ctx?: any): EventRef;
```

### on

```ts
on(name: 'closed', callback: () => any, ctx?: any): EventRef;
```
