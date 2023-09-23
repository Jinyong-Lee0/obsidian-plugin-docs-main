---
sidebar_position: 40
---

# Vault

[여러 볼트로 작업하기] 공식 문서(https://help.obsidian.md/How+to/Working+with+multiple+vaults)에서 발췌한 내용입니다:

> 흑요석의 각 노트 모음을 볼트라고 합니다. 볼트는 폴더와 그 안의 하위 폴더로 구성됩니다.

플러그인은 다른 Node.js 애플리케이션처럼 파일 시스템에 액세스할 수 있지만, [`Vault`](./reference/typescript/classes/Vault.md) 모듈은 Vault 안의 파일과 폴더 작업을 더 쉽게 하는 것을 목표로 합니다.

다음 예제는 Vault에 있는 모든 마크다운 파일의 경로를 재귀적으로 출력합니다:

```ts
const files = this.app.vault.getMarkdownFiles();

for (let i = 0; i < files.length; i++) {
    console.log(files[i].path);
}
```

:::팁
마크다운 문서뿐만 아니라 _모든_ 파일을 나열하려면, 대신 [`getFiles()`](./reference/typescript/classes/Vault.md#getfiles)를 사용하세요.
:::

## 파일 읽기

## 파일 읽기

파일의 내용을 읽는 방법에는 두 가지가 있습니다: [`read()`](./reference/typescript/classes/Vault.md#read) 및 [`cachedRead()`](./reference/typescript/classes/Vault.md#cachedread).

-   사용자에게 콘텐츠만 표시하려는 경우 디스크에서 파일을 여러 번 읽지 않도록 `cachedRead()`를 사용하십시오.
-   콘텐츠를 읽고 변경한 다음 디스크에 다시 쓰려면 `read()`를 사용하여 오래된 복사본으로 파일을 덮어쓰는 것을 방지하세요.

:::정보
`cachedRead()`와 `read()`의 유일한 차이점은 플러그인이 파일을 읽기 직전에 옵시디언 외부에서 파일을 수정한 경우입니다. 파일 시스템이 외부에서 파일이 변경되었음을 옵시디언에 알리는 즉시 `cachedRead()`는 `read()`처럼 _정확하게_ 동작합니다. 마찬가지로, 옵시디언 내에서 파일을 저장하면 읽기 캐시도 함께 플러시됩니다.
:::

다음 예제는 Vault에 있는 모든 마크다운 파일의 내용을 읽고 평균 문서 크기를 반환합니다:

```ts title="main.ts"
import { Notice, Plugin } from "obsidian";

export default class ExamplePlugin extends Plugin {
    async onload() {
        this.addRibbonIcon(
            "info",
            "Calculate average file length",
            async () => {
                const fileLength = await this.averageFileLength();
                new Notice(
                    `The average file length is ${fileLength} characters.`
                );
            }
        );
    }

    async averageFileLength(): Promise<number> {
        const { vault } = this.app;

        const fileContents: string[] = await Promise.all(
            vault.getMarkdownFiles().map((file) => vault.cachedRead(file))
        );

        let totalLength = 0;
        fileContents.forEach((content) => {
            totalLength += content.length;
        });

        return totalLength / fileContents.length;
    }
}
```

## 파일 삭제

파일을 삭제하는 메서드에는 [`delete()`](./reference/typescript/classes/Vault.md#delete)와 [`trash()`](./reference/typescript/classes/Vault.md#trash)의 두 가지가 있습니다. 어떤 것을 사용해야 하는지는 사용자가 마음을 바꿀 수 있도록 하느냐에 따라 달라집니다.

-   delete()`는 파일을 흔적 없이 제거합니다.
-   trash()`는 파일을 휴지통으로 이동합니다.

trash()`를 사용하면 파일을 시스템의 휴지통으로 옮길지, 아니면 사용자 Vault의 루트에 있는 로컬 `.trash` 폴더로 옮길지 선택할 수 있습니다.

## 파일인가, 폴더인가?

일부 연산은 파일 또는 폴더일 수 있는 [`TAbstractFile`](./reference/typescript/classes/TAbstractFile.md) 객체를 반환하거나 수락합니다. 사용하기 전에 항상 `TAbstractFile`의 구체적인 유형을 확인하십시오.

```ts
const folderOrFile = this.app.vault.getAbstractFileByPath("folderOrFile");

if (folderOrFile instanceof TFile) {
    console.log("It's a file!");
} else if (folderOrFile instanceof TFolder) {
    console.log("It's a folder!");
}
```
