---
sidebar_position: 110
---

# 개발자 도구

이 페이지에서는 플러그인 개발자를 위한 도구들을 나열합니다. 이 도구들은 플러그인 개발에 필수적이지는 않지만, 플러그인 개발을 간소화할 수 있습니다.

## Obsidian Tools

[Obsidian Tools](https://github.com/obsidian-tools/obsidian-tools)은 플러그인 개발자를 위한 도구 모음입니다.

## 모든 플러그인 로컬로 다운로드하기

문제가 발생할 경우, 다른 사람들이 어떻게 해결했는지 확인하는 것이 도움이 될 수 있습니다. 컴퓨터에 전체 플러그인 라이브러리를 다운로드하여 소스 코드를 검색하여 영감을 얻을 수 있습니다.

-   [konhi/obsidian-repositories-downloader](https://github.com/konhi/obsidian-repositories-downloader)
-   [luckman212/obsidian-plugin-downloader](https://github.com/luckman212/obsidian-plugin-downloader)
-   [claremacrae/obsidian-repos-downloader](https://github.com/claremacrae/obsidian-repos-downloader)

## 베타 테스트

플러그인을 [게시](publishing/submit-your-plugin.md)하기 전에 사용자가 먼저 시도해 볼 수 있도록 할 수도 있습니다.

[BRAT](https://github.com/TfTHacker/obsidian42-brat) 플러그인을 사용하면, 베타 테스터들은 아직 게시되지 않은 플러그인을 설치할 수 있습니다.

## 배지

플러그인의 다운로드 수를 나타내는 배지를 추가하려면, 다음 내용을 README에 붙여넣고 `<PLUGIN_ID>`를 플러그인 ID로 대체하세요:

```md
![Obsidian Downloads](https://img.shields.io/badge/dynamic/json?logo=obsidian&color=%23483699&label=downloads&query=%24%5B%22<PLUGIN_ID>%22%5D.downloads&url=https%3A%2F%2Fraw.githubusercontent.com%2Fobsidianmd%2Fobsidian-releases%2Fmaster%2Fcommunity-plugin-stats.json)
```

예를 들어, Calendar 플러그인의 다운로드 수는 다음과 같습니다:

![Obsidian Downloads](https://img.shields.io/badge/dynamic/json?logo=obsidian&color=%23483699&label=downloads&query=%24%5B%22calendar%22%5D.downloads&url=https%3A%2F%2Fraw.githubusercontent.com%2Fobsidianmd%)
