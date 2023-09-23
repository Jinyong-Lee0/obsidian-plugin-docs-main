# Manifest

이 페이지에서는 플러그인 매니패스트(`manifest.json`)의 스키마를 설명합니다.

## Properties

| 속성            | 타입    | 필수     | 설명                                                  |
| --------------- | ------- | -------- | ----------------------------------------------------- |
| `author`        | string  | **필수** | 플러그인 작성자의 이름.                               |
| `description`   | string  | **필수** | 플러그인에 대한 상세한 설명.                          |
| `id`            | string  | **필수** | 플러그인 ID.                                          |
| `isDesktopOnly` | boolean | **필수** | 플러그인이 NodeJS 또는 Eletron API를 사용하는지 여부. |
| `minAppVersion` | string  | **필수** | 플러그인을 위해 필요한 푀소 Obsidian 버전.            |
| `name`          | string  | **필수** | 플러그인의 화면에 나타나는 이름.                      |
| `version`       | string  | **필수** | 플러그인 버전.                                        |
| `authorUrl`     | string  | No       | 저자의 URL.                                           |
| `fundingUrl`    | string  | No       | 프로젝트 지원 URL.                                    |
