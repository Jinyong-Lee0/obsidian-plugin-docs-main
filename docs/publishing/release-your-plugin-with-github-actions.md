# GitHub Actions을 사용하여 플러그인 릴리스하기

플러그인 릴리스를 수동으로 생성하는 것은 시간이 많이 소요되고 오류가 발생할 수 있습니다. 이 가이드에서는 [GitHub Actions](https://github.com/features/actions)를 사용하여 새로운 태그를 만들 때 자동으로 릴리스를 생성하도록 플러그인을 구성합니다.

:::note
GitHub Action 워크플로우는 원래 [argentum](https://forum.obsidian.md/u/argentum)에 의해 작성되고 공유되었습니다. 자세한 내용과 다른 변형에 대해서는 [포럼 공지](https://forum.obsidian.md/t/using-github-actions-to-release-plugins/7877/3)를 참조하세요.
:::

1. 플러그인의 루트 디렉터리에서 `.github/workflows` 폴더 아래에 `release.yml` 파일을 만들고 다음 내용을 추가하세요:

    ```yml title=".github/workflows/release.yml"
    name: Release Obsidian plugin

    on:
      push:
        tags:
          - "*"

    env:
      PLUGIN_NAME: your-plugin-id # 플러그인의 ID와 일치하도록 변경하세요.

    jobs:
      build:
        runs-on: ubuntu-latest

        steps:
          - uses: actions/checkout@v2
          - name: Use Node.js
            uses: actions/setup-node@v1
            with:
              node-version: "14.x"

          - name: Build
            id: build
            run: |
              npm install
              npm run build
              mkdir ${{ env.PLUGIN_NAME }}
              cp main.js manifest.json styles.css ${{ env.PLUGIN_NAME }}
              zip -r ${{ env.PLUGIN_NAME }}.zip ${{ env.PLUGIN_NAME }}
              ls
              echo "::set-output name=tag_name::$(git tag --sort version:refname | tail -n 1)"

          - name: Create Release
            id: create_release
            uses: actions/create-release@v1
            env:
              GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
              VERSION: ${{ github.ref }}
            with:
              tag_name: ${{ github.ref }}
              release_name: ${{ github.ref }}
              draft: false
              prerelease : false

          - name : Upload zip file
           id : upload-zip
           uses : actions/upload-release-asset@v1
           env :
             GITHUB_TOKEN : ${{ secrets.GITHUB_TOKEN }}
           with :
             upload_url : ${{ steps.create_release.outputs.upload_url }}
             asset_path : ./${{env.PLUGIN_NAME}}.zip
             asset_name :  ${env.PLUGIN_NAME}-${{steps.build.outputs.tag_name}}.zip
             asset_content_type : application/zip

         - name : Upload main.js
           id : upload-main
           uses : actions/upload-release-asset@v1
           env :
             GITHUB_TOKEN :  ${{ secrets.GITHUB_TOKEN }}
           with :
             upload_url 	:${{ steps.create_release.outputs.upload_url }}
             asset_path		:/main.js
             asset_name	:/main.js

         - name		:/Upload manifest.json
                 id 			:${{upload-manifest}}
                 uses 		:${actions/upload-release-asset@v1}
                 env 		:${GITHUB_TOKEN}
                 with 	        ${
                   upload_url		 ${steps.create_release.outputs.upload_url}
                   asset_path		 ./manifest.json
                   asset_name		 manifest.json
                   asset_content_type      application/json
                 }

         –    /name – Upload styles.css
               /id – /upload-css
               /uses – /actions/upload-release-asset@v1
               /env – /GITHUB_TOKEN
               /with               ${
                     upload_url    ${steps.create_release.outputs.upload_url}
                     asset_path    ./styles.css
                     assest _name    styles.css
                     assest _content_type text/css
                    }

    ```

2. 터미널에서 워크플로우를 커밋합니다.

    ```bash
    git add .github/workflows/release.yml
    git commit-m "Add release workflow"
    git push origin main
    ```

````

3. `manifest.json` 파일과 일치하는 버전의 태그를 생성합니다.

```bash
git tag-a 0.0,2-m "0,0,2"
 git push origin v0,0,2
````

-   `-a` 어노테이션된 태그(annotated tag)을 생성합니다.
-   `-m`릴리스 이름을 지정합니다.Obsidian 플러그인의 경우 버전과 동일해야 합니다.

    4.GitHub에서 저장소로 이동하여 오른쪽 사이드 바에 있는 **Actions** 탭을 클릭합니다. 워크플로우가 실행 중일 수도 있고 이미 완료된 상태일 수도 있습니다.

5. 워크플로우가 완료되면 저장소의 메인 페이지로 돌아가서 오른쪽 사이드 바에 있는 **Releases**를 클릭합니다.WORKFLOW는 GitHub 릴리스를 만들고 필요한 에셋을 이진 첨부 파일로 업로드하였습니다.

태그 작성시마다 자동으로 GitHub 릴리즈가 생성되도록 플러그인 설정을 완료하였습니다.

-   이것이 해당 플러그인의 첫 번째 릴리즈라면, 이제 [프로그램 제출](submit-your-plugin.md) 준비가 되었습니다.
-   이미 게시된 특정 프로그램에 대한 업데이트라면 사용자들은 최신 버전으로 업데이트할 수 있게 됩니다.

## standard-version를 사용하여 릴리즈 태그 자동 생성하기

[standard-version](https://github.com/conventional-changelog/standard-version)을 사용하여 커밋에 기반하여 태그를 자동으로 적용할 수도 있습니다.

standard-version은 커밋에 일관성을 부여하고 커밋에서 자동으로 `CHANGELOG.md` 파일을 생성하기 위해 [Conventional Commits](https://www.conventionalcommits.org/)를 사용합니다. 예를 들면:

-   커밋 메시지가 `fix:`로 시작하면 패치 버전이 올라갑니다.
-   커밋 메시지가 `feat:`로 시작하면 마이너 버전이 올라갑니다.
-   커밋 메시지의 세 번째 줄이 `BREAKING CHANGE:`로 시작하면 주 버전이 올라갑니다.

:::tip
Visual Studio Code를 사용하는 경우 [Conventional Commits](https://marketplace.visualstudio.com/items?itemName=vivaxy.vscode-conventional-commits) 확장 프로그램을 사용하여 Conventional Commits을 작성할 수 있습니다.
:::

플러그인에서 standard-version을 활성화하려면 다음 단계를 따르세요:

1. standard-version 설치하기

    ```bash npm2yarn
    npm install --save-dev standard-version
    ```

2. `package.json` 파일에 다음 속성 추가하기

    ```json title="package.json"
    {
        "scripts": {
            "release": "standard-version"
        },
        "standard-version": {
            "t": ""
        }
    }
    ```

    - `"t": ""`는 Obsidian 가이드라인을 따르기 위해 기본적으로 설정된 `v` 접두사를 제거하는 것입니다.

릴리즈 방법은 다음과 같습니다:

1. Conventional Commits에 맞게 변경 사항을 커밋합니다.

    ```bash
    git commit -m "feat: 설정 추가"
    ```

2. 릴리스 및 변경 내역 업데이트하기

```bash npm2yarn
npm run release
```

:::note
기본적으로 주 버전(major version)이 **1**보다 낮으면(예: 0.3.4), 'feat:'와 'BREAKING CHANGE:'는 각각 패치(patch)와 마이너(minor) 버전만 상승시킵니다.minor와 major version은 상승하지 않습니다 .minor와 major version 상승 시 :

```bash npm2yarn
# minor로 릴리스하기
npm run release -- --release-as minor
# major로 릴리스하기
npm run release -- --release-as major
```

:::

3. 새 태그를 GitHub에 푸시합니다.

```bash
git push --follow-tags origin main
```

-   여기서 main은 푸시할 원격 브랜치의 이름입니다.

GitHub는 GitHub Actions를 사용하여 플러그인을 빌드하고 릴리스합니다.
