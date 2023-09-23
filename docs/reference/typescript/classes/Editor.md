# Editor

CodeMirror 5와 CodeMirror 6 사이의 간격을 메우는 공통 인터페이스입니다.

## Constructor

```ts
constructor();
```

## Methods

### getDoc

```ts
getDoc(): this;
```

### refresh

```ts
abstract refresh(): void;
```

### getValue

```ts
abstract getValue(): string;
```

### setValue

```ts
abstract setValue(content: string): void;
```

### getLine

```ts
abstract getLine(line: number): string;
```

줄로 텍스트 가져오기(0 색인)

### setLine

```ts
setLine(n: number, text: string): void;
```

### lineCount

```ts
abstract lineCount(): number;
```

문서의 줄 수를 가져옵니다

### lastLine

```ts
abstract lastLine(): number;
```

### getSelection

```ts
abstract getSelection(): string;
```

### somethingSelected

```ts
somethingSelected(): boolean;
```

### getRange

```ts
abstract getRange(from: EditorPosition, to: EditorPosition): string;
```

### replaceSelection

```ts
abstract replaceSelection(replacement: string, origin?: string): void;
```

### replaceRange

```ts
abstract replaceRange(replacement: string, from: EditorPosition, to?: EditorPosition, origin?: string): void;
```

### getCursor

```ts
abstract getCursor(string?: 'from' | 'to' | 'head' | 'anchor'): EditorPosition;
```

### listSelections

```ts
abstract listSelections(): EditorSelection[];
```

### setCursor

```ts
setCursor(pos: EditorPosition | number, ch?: number): void;
```

### setSelection

```ts
abstract setSelection(anchor: EditorPosition, head?: EditorPosition): void;
```

### setSelections

```ts
abstract setSelections(ranges: EditorSelectionOrCaret[], main?: number): void;
```

### focus

```ts
abstract focus(): void;
```

### blur

```ts
abstract blur(): void;
```

### hasFocus

```ts
abstract hasFocus(): boolean;
```

### getScrollInfo

```ts
abstract getScrollInfo(): {
    top: number;
    left: number;
};
```

### scrollTo

```ts
abstract scrollTo(x?: number | null, y?: number | null): void;
```

### scrollIntoView

```ts
abstract scrollIntoView(range: EditorRange, center?: boolean): void;
```

### undo

```ts
abstract undo(): void;
```

### redo

```ts
abstract redo(): void;
```

### exec

```ts
abstract exec(command: EditorCommandName): void;
```

### transaction

```ts
abstract transaction(tx: EditorTransaction, origin?: string): void;
```

### wordAt

```ts
abstract wordAt(pos: EditorPosition): EditorRange | null;
```

### posToOffset

```ts
abstract posToOffset(pos: EditorPosition): number;
```

### offsetToPos

```ts
abstract offsetToPos(offset: number): EditorPosition;
```

### processLines

```ts
processLines<T>(read: (line: number, lineText: string) => T | null, write: (line: number, lineText: string, value: T | null) => EditorChange | void, ignoreEmpty?: boolean): void;
```
