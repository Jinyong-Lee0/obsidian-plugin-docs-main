---
sidebar_position: 1
---

# 플러그인 제출하기

Obsidian 커뮤니티와 플러그인을 공유하려면 플러그인을 [공식 플러그인 목록](https://github.com/obsidianmd/obsidian-releases/blob/master/community-plugins.json)에 제출하는 것이 가장 좋습니다. 플러그인이 검토된 후에는 사용자가 Obsidian 내에서 직접 플러그인을 설치할 수 있습니다. 또한 Obsidian 웹 사이트의 [플러그인 디렉터리](https://obsidian.md/plugins)에도 게시됩니다. 이 가이드에서는 자체 플러그인을 제출하는 방법을 안내합니다.

:::caution
이 가이드의 목적은 보다 상세한 지침을 제공하는 것입니다. 그럼에도 불구하고, 플러그인을 제출하기 전에 반드시 [공식 지침](https://github.com/obsidianmd/obsidian-sample-plugin#adding-your-plugin-to-the-community-plugin-list)를 검토하여야 합니다.
:::

## 사전 준비 작업

본 안내서를 따르기 위해서는 다음 파일들이 저장소의 루트 경로에 있어야 합니다:

-   `README.md`: 플러그인의 목적과 사용 방법에 대해 설명하는 파일입니다.
-   `LICENSE`: 다른 사람들이 플러그인과 소스 코드를 어떻게 사용할 수 있는지를 결정하는 파일입니다. 라이선스 선택에 도움이 필요한 경우 [Choose a License](https://choosealicense.com/)를 참조하세요.
-   `manifest.json`: 플러그인을 설명하는 파일입니다. 자세한 내용은 [Manifest](reference/manifest.md)를 참조하세요.

## 단계 1 — 릴리스 생성하기

본 단계에서는 제출할 준비가 완료된 플러그인용 릴리스를 준비합니다.

1. `manifest.json`에서 `version` 속성값을 [Semantic Versioning](https://semver.org/) 규격에 맞춰 새로운 버전으로 업데이트합니다.

2. GitHub에서 [릴리즈 생성하기](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository#creating-a-release).

    - "Tag version"은 `manifest.json` 파일의 버전과 일치해야 합니다.
    - 태그 버전에서 `v`는 포함하지 않아야 합니다.

3. 릴리즈 이름과 설명 입력란 작성하기.

4. 다음 프로그램 에셋들을 바이너리 첨부판으로서 해당 릴리즈로 업로드합니다:
    - `main.js`
    - `manifest.json`
    - (옵션) `styles.css`

:::tip
릴리즈 생성 프로세스 자동화 방법은 [GitHub Actions으로 Plugin Release 생성하기](release-your-plugin-with-github-actions.md) 문서를 참조하세요.
:::

## 단계 2 — 리뷰 요청 및 제출

본 단계에서는 Obsidian 개발팀에게 리뷰 요청 및 제출 작업을 진행합니다.

1. GitHub에서 [obsidian-releases 저장소](https://github.com/obsidianmd/obsidian-releases)를 fork합니다.[Fork a repo](<(https://docs.github.com/en/get-started/quickstart/fork-a-repo)>) 문서에서 저장소 fork 방법에 대해 확인하세요.

2.`community-plugins.json`파일 안 JSON 배열안 새롭게 등록하고자 하는 내용 추가한다음 PR(Pull Request)생성한다.(아래 예제 참조)

```json
{
    "id": "recent-files-obsidian",
    "name": "Recent Files",
    "author": "Tony Grosinger",
    "description": "Display a list of recently opened files",
    "repo": "tgrosinger/recent-files-obsidian",
    "branch": "main"
}
```

-   id, name, author 및 description : 이것은 유저 환경앱상 나타나며 manifest 의 속성값과 일치되어야 한다.
    id : 여기서 중요한건 고유해야 한다 .community-plugins.json 에 기존 id가 없으면 확인 해보세요
    repo : 여기서 중요한건 github repository 의 주소여야 한다 . 예외적으로 gitlab 혹은 bitbucket 도 가능하나 github 가 대부분 입니다 .
    branch (optional): 여기선 git branch 의 이름 입니다 기본 값은 master 입니다 .

마지막 brace , } 후 comma , 넣어주기 3.[Create a pull request](<(https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)>)문서참고해서 PR생성한다 .

4.PR 만들 때 description field 지침대로 하여 해당 template 로 PR생성한다 .
5.Create pull request 클릭한다 .
6.Pull request 상세내용 입력하라고 되어있다면 입력한다 . checkbox 로 체크박스는 done 으로 처리되므로 각각 []앞 x 넣으면 됩니다 .
7.Create pull request 클릭한다.(마지막번 🤞).

이제 플러그인을 Obsidian 플러그인 디렉토리에 제출했습니다. 팀이 플러그인을 검토했을 때까지 기다리세요. 플러그인의 검토 시간은 Obsidian 팀의 현재 작업량에 따라 달라집니다. Obsidian 팀은 아직 작은 규모이므로, 플러그인 검토가 완료될 때까지 기다리는 동안 양해 부탁드립니다.

## 단계 3 — 리뷰 코멘트에 대응하기

리뷰어가 플러그인을 검토했을 때, 그 결과를 코멘트로 pull request에 남길 것입니다. 리뷰어는 당신의 플러그인 업데이트를 요청하거나 개선 방법에 대한 제안을 할 수 있습니다.

플러그인 게시는 Obsidian 팀 멤버만 가능하지만, 다른 커뮤니티 구성원들도 임시로 제출한 내용을 검토하는 데 도움을 줄 수 있습니다.

pull request가 병합된 후 사용자들은 바로 해당 프로그램 설치할 수 있게 됩니다.

:::tip 도움이 필요하세요?
커뮤니티 프로그램 리뷰를 돕고 싶으시다면 [Plugin Review Guidelines](https://liamca.in/Obsidian/Plugin+Review+Guide/index) 문서를 참조하세요.
:::

## 이미 게시된 프로그램 업데이트하기

초기 버전의 프로그램만 제출하면 됩니다. 그 이후 사용자들은 Obsidian 내에서 자동으로 새로운 업데이트를 다운로드할 수 있습니다.

새 버전의 프로그램을 릴리즈하려면 [릴리즈 생성하기](#step-1--create-a-release) 안내사항을 따르세요.

커뮤니티 프로그램의 새 버전이 어떻게 Obsidian에서 가져오는지 자세한 정보는 [How community plugins are pulled](https://github.com/obsidianmd/obsidian-releases#how-community-plugins-are-pulled) 문서를 참조하세요.
