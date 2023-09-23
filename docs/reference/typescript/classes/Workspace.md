# Workspace

Extends `Events`

## Constructor

```ts
constructor();
```

## Properties

### leftSplit

```ts
leftSplit: WorkspaceSidedock | WorkspaceMobileDrawer;
```

### rightSplit

```ts
rightSplit: WorkspaceSidedock | WorkspaceMobileDrawer;
```

### leftRibbon

```ts
leftRibbon: WorkspaceRibbon;
```

### rightRibbon

```ts
rightRibbon: WorkspaceRibbon;
```

### rootSplit

```ts
rootSplit: WorkspaceRoot;
```

### activeLeaf

```ts
activeLeaf: WorkspaceLeaf;
```

현재 포커스가 맞춰진 leaf(리프)를 가리킵니다, 만약 존재한다면.

`activeLeaf`를 직접 사용하는 것을 피해 주세요, 특히 `activeLeaf`가 null인지 확인하지 않고 사용하는 경우는 더욱 그렇습니다.

권장되는 대안은 다음과 같습니다:

-   현재 뷰에 대한 정보가 필요한 경우, {@link getActiveViewOfType}를 사용하세요.
-   새 파일을 열거나 뷰를 탐색해야 하는 경우, {@link getLeaf}를 사용하세요.

### containerEl

```ts
containerEl: HTMLElement;
```

### layoutReady

```ts
layoutReady: boolean;
```

### requestSaveLayout

```ts
requestSaveLayout: Debouncer<[], Promise<void>>;
```

### activeEditor

```ts
activeEditor: MarkdownFileInfo;
```

현재 에디터를 관리하는 컴포넌트입니다. 활성 뷰에 에디터가 없는 경우 null이 될 수 있습니다.

## 메소드들

### onLayoutReady

```ts
onLayoutReady(callback: () => any): void;
```

레이아웃이 이미 준비되어 있다면 콜백 함수를 즉시 실행하거나, 레이아웃이 준비될 때까지 나중에 호출될 수 있도록 큐에 넣습니다.

### changeLayout

```ts
changeLayout(workspace: any): Promise<void>;
```

### getLayout

```ts
getLayout(): any;
```

### createLeafInParent

```ts
createLeafInParent(parent: WorkspaceSplit, index: number): WorkspaceLeaf;
```

### createLeafBySplit

```ts
createLeafBySplit(leaf: WorkspaceLeaf, direction?: SplitDirection, before?: boolean): WorkspaceLeaf;
```

### splitActiveLeaf

```ts
splitActiveLeaf(direction?: SplitDirection): WorkspaceLeaf;
```

### duplicateLeaf

```ts
duplicateLeaf(leaf: WorkspaceLeaf, direction?: SplitDirection): Promise<WorkspaceLeaf>;
```

### duplicateLeaf

```ts
duplicateLeaf(leaf: WorkspaceLeaf, leafType: PaneType | boolean, direction?: SplitDirection): Promise<WorkspaceLeaf>;
```

### getUnpinnedLeaf

```ts
getUnpinnedLeaf(type?: string): WorkspaceLeaf;
```

### getLeaf

```ts
getLeaf(newLeaf?: 'split', direction?: SplitDirection): WorkspaceLeaf;
```

현재 활성화된 leaf에 인접한 leaf에 새로운 leaf를 생성합니다.
direction이 `'vertical'`이면, leaf는 오른쪽에 나타납니다.
direction이 `'horizontal'`이면, leaf는 현재 leaf 아래에 나타납니다.
newLeaf가 false(또는 설정되지 않았다면) 이동 가능한 기존의 leaf를 반환하거나, 사용 가능한 leaf가 없었다면 새로운 leaf를 생성합니다.

newLeaf가 `'tab'` 또는 `true`라면 root split 내의 선호하는 위치에 새로운 리프가 생성되어 반환됩니다.

newLeaf가 `'split'`라면 현재 활성화된 리프와 인접해 새로운 리프가 생성됩니다.

newLeaf가 `'window'`라면 팝아웃 창 안에 새로운 리프를 가진 창이 생성됩니다.

### getLeaf

```ts
getLeaf(newLeaf?: PaneType | boolean): WorkspaceLeaf;
```

현재 활성화된 리프와 인접해 있는 리프 안에 새로운 리프를 만듭니다.
만약 direction이 'vertical' 이라면, 리프는 오른쪽으로 나타날 것입니다.
만약 direction이 'horizontal' 이라면, 현재의 리프 아래에서 나타날 것입니다.
만약 newleaf 가 false (또는 설정되지 않은 경우), 탐색 가능한 기존의 리프를 반환하거나, 사용 가능한 다른 리프가 없다면 새롭게 만들어집니다.

newleaf 가 'tab' 또는 true인 경우 root split 내에서 선호하는 위치에서 새롭게 만들어집니다.

newleaf 가 'split'인 경우 현재 활성화된 leaf와 인접하여 새롭게 만들어집니다.

newleaf 가 'window'인 경우 팝아웃 윈도우 안에서 신규 Leaf 로 구성된 창을 생성합니다.

### moveLeafToPopout

```ts
moveLeafToPopout(leaf: WorkspaceLeaf, data?: WorkspaceWindowInitData): WorkspaceWindow;
```

해당 Leaf를 새 팝아웃 창으로 이동시깁니다.
단지 데스크탑 앱에서만 작동합니다.

### openPopoutLeaf

```ts
openPopoutLeaf(data?: WorkspaceWindowInitData): WorkspaceLeaf;
```

단일 새 Leaf와 함께 새 팝아웃 창을 열고 해당 Leaf를 반환합니다.
단지 데스크탑 앱에서만 작동합니다.

### openLinkText

```ts
openLinkText(linktext: string, sourcePath: string, newLeaf?: PaneType | boolean, openViewState?: OpenViewState): Promise<void>;
```

### setActiveLeaf

```ts
setActiveLeaf(leaf: WorkspaceLeaf, params?: {
    focus?: boolean;
}): void;
```

리프를 활성상태로 설정합니다

### setActiveLeaf

```ts
setActiveLeaf(leaf: WorkspaceLeaf, pushHistory: boolean, focus: boolean): void;
```

리프를 활성상태로 설정합니다

### getLeafById

```ts
getLeafById(id: string): WorkspaceLeaf;
```

### getGroupLeaves

```ts
getGroupLeaves(group: string): WorkspaceLeaf[];
```

### getMostRecentLeaf

```ts
getMostRecentLeaf(root?: WorkspaceParent): WorkspaceLeaf | null;
```

### getLeftLeaf

```ts
getLeftLeaf(split: boolean): WorkspaceLeaf;
```

### getRightLeaf

```ts
getRightLeaf(split: boolean): WorkspaceLeaf;
```

### getActiveViewOfType

```ts
getActiveViewOfType<T extends View>(type: Constructor<T>): T | null;
```

### getActiveFile

```ts
getActiveFile(): TFile | null;
```

현재 뷰가 FileView라면 해당 파일을 반환합니다.

그렇지 않다면, 가장 최근에 활성화된 파일을 반환합니다.

### iterateRootLeaves

```ts
iterateRootLeaves(callback: (leaf: WorkspaceLeaf) => any): void;
```

워크스페이스의 주 영역에 있는 모든 leaf를 순회합니다.

### iterateAllLeaves

```ts
iterateAllLeaves(callback: (leaf: WorkspaceLeaf) => any): void;
```

주 영역의 leaf, 플로팅 leaf, 사이드바 leaf를 포함한 모든 leaf를 순회합니다.

### getLeavesOfType

```ts
getLeavesOfType(viewType: string): WorkspaceLeaf[];
```

### detachLeavesOfType

```ts
detachLeavesOfType(viewType: string): void;
```

### revealLeaf

```ts
revealLeaf(leaf: WorkspaceLeaf): void;
```

### getLastOpenFiles

```ts
getLastOpenFiles(): string[];
```

### updateOptions

```ts
updateOptions(): void;
```

Calling this function will update/reconfigure the options of all markdown panes.
It is fairly expensive, so it should not be called frequently.

### iterateCodeMirrors

```ts
iterateCodeMirrors(callback: (cm: CodeMirror.Editor) => any): void;
```

### on

```ts
on(name: 'quick-preview', callback: (file: TFile, data: string) => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'resize', callback: () => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'click', callback: (evt: MouseEvent) => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'active-leaf-change', callback: (leaf: WorkspaceLeaf | null) => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'file-open', callback: (file: TFile | null) => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'layout-change', callback: () => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'window-open', callback: (win: WorkspaceWindow, window: Window) => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'window-close', callback: (win: WorkspaceWindow, window: Window) => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'css-change', callback: () => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'file-menu', callback: (menu: Menu, file: TAbstractFile, source: string, leaf?: WorkspaceLeaf) => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'editor-menu', callback: (menu: Menu, editor: Editor, info: MarkdownView | MarkdownFileInfo) => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'editor-change', callback: (editor: Editor, info: MarkdownView | MarkdownFileInfo) => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'editor-paste', callback: (evt: ClipboardEvent, editor: Editor, info: MarkdownView | MarkdownFileInfo) => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'editor-drop', callback: (evt: DragEvent, editor: Editor, info: MarkdownView | MarkdownFileInfo) => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'codemirror', callback: (cm: CodeMirror.Editor) => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.

### on

```ts
on(name: 'quit', callback: (tasks: Tasks) => any, ctx?: any): EventRef;
```

앱의 CSS가 변경되었을 때 발생합니다.
사용자가 파일에서 컨텍스트 메뉴를 열었을 때 발생합니다.
사용자가 에디터에서 컨텍스트 메뉴를 열었을 때 발생합니다.
에디터에 변화가 적용되었을 때(프로그래밍적으로 또는 사용자 이벤트로 인해) 발생합니다.
에디터가 붙여넣기 이벤트를 받았을 때 발생합니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()`를 사용하여 이벤트를 처리했다는 것을 나타내야 합니다.
에디터가 드롭 이벤트를 받았을 때 트리거됩니다.
이 이벤트를 처리하기 전에 `evt.defaultPrevented`를 확인하고 이미 처리된 경우 반환해야 합니다.
`evt.preventDefault()` 를 사용하여 이벤트 처리 완료 상태임을 표시해야 합니다.
앱 종료 직전에 트리거 될 수 있습니다. 반드시 실행되는 것은 아닙니다.
여기서 최선의 노력으로 정리 작업을 수행하세요.
