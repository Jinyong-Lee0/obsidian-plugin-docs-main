# MarkdownPostProcessor

포스트 프로세서는 미리보기의 섹션인 요소를 받아옵니다.

포스트 프로세서는 DOM을 변경하여 다양한 요소(예: mermaid 그래프, LaTeX 방정식, 사용자 정의 컨트롤 등)를 렌더링할 수 있습니다.

만약 포스트 프로세서가 수명 주기 관리를 필요로 한다면, 예를 들어 이 요소가 앱에서 제거될 때 인터벌을 해제하거나 서브프로세스를 종료하는 경우에는 {@link MarkdownPostProcessorContext#addChild}을 확인해보세요.

## 속성

### sortOrder

```ts
sortOrder: number;
```

선택적인 정수형 정렬 순서입니다. 기본값은 0입니다. 낮은 숫자일수록 높은 숫자보다 먼저 실행됩니다.
