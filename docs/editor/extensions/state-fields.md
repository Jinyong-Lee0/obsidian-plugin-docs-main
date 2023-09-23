---
sidebar_position: 2
---

# 상태 필드

상태 필드는 사용자 정의 편집기 상태를 관리할 수 있는 [편집기 확장](index.md)입니다. 이 페이지에서는 계산기 확장을 구현하여 상태 필드를 구축하는 방법을 안내합니다.

계산기는 현재 상태에서 숫자를 더하고 빼고, 다시 시작할 때 상태를 재설정할 수 있어야 합니다.

이 페이지의 끝까지 따라오면, 상태 필드를 구축하는 기본 개념을 이해하게 될 것입니다.

:::note
이 페이지는 Obsidian 플러그인 개발자를 위한 공식 CodeMirror 6 문서를 단순화한 내용입니다. 상태 필드에 대한 자세한 정보는 [State Fields](https://codemirror.net/docs/guide/#state-fields)를 참조하세요.
:::

## 전제 조건

-   [상태 관리](state-management.md)에 대한 기본적인 이해.

## 상태 효과 정의하기

상태 효과(State effects)는 적용하려는 상태 변경을 설명합니다. 클래스의 메서드와 같은 것으로 생각할 수 있습니다.

계산기 예제에서 각 계산 작업에 대해 하나씩의 상태 효과(State effect)를 정의합니다:

```ts
const addEffect = StateEffect.define<number>();
const subtractEffect = StateEffect.define<number>();
const resetEffect = StateEffect.define();
```

꺾쇠 괄호(`<>`) 사이의 타입은 효과에 대한 입력 타입을 정의합니다. 예를 들어, 더하거나 빼려는 숫자입니다. 재설정 효과에는 입력이 필요하지 않으므로 생략할 수 있습니다.

## 상태 필드 정의하기

상태 필드(State field)는 실제로 상태를 *저장*하는 것이 아니라, 상태를 *관리*합니다. 상태 필드는 현재 상태를 가져와서 모든 상태 효과(State effect)를 적용하고 새로운 상태를 반환합니다.

상태 필드에는 트랜잭션 내에서 수학 연산을 적용하는 계산기 로직이 포함되어 있습니다. 트랜잭션에는 여러 개의 효과가 포함될 수 있으므로, 예를 들어 두 개의 덧셈일 경우, 상태 필드에서 모두 하나씩 차례대로 적용해야 합니다.

```ts
export const calculatorField = StateField.define<number>({
    create(state: EditorState): number {
        return 0;
    },
    update(oldState: number, transaction: Transaction): number {
        let newState = oldState;

        for (let effect of transaction.effects) {
            if (effect.is(addEffect)) {
                newState += effect.value;
            } else if (effect.is(subtractEffect)) {
                newState -= effect.value;
            } else if (effect.is(resetEffect)) {
                newState = 0;
            }
        }

        return newState;
    },
});
```

-   `create`는 계산기가 시작할 때 사용하는 값을 반환합니다.
-   `update`에는 효과를 적용하는 로직이 포함되어 있습니다.
-   `effect.is()`를 사용하여 효과를 적용하기 전에 효과의 유형을 확인할 수 있습니다.

## 상태 효과 디스패치하기

상태 필드에 상태 효과를 적용하려면, 해당 효과를 에디터 뷰로 전달하여 트랜잭션의 일부로 디스패치해야 합니다.

```ts
view.dispatch({
    effects: [addEffect.of(num)],
});
```

더욱 익숙한 API를 제공하는 도우미 함수 집합을 정의할 수도 있습니다:

```ts
export function add(view: EditorView, num: number) {
    view.dispatch({
        effects: [addEffect.of(num)],
    });
}

export function subtract(view: EditorView, num: number) {
    view.dispatch({
        effects: [subtractEffect.of(num)],
    });
}

export function reset(view: EditorView) {
    view.dispatch({
        effects: [resetEffect.of(null)],
    });
}
```

## 다음 단계

[상태 필드](decorations.md)에서 제공된 장식을 사용하여 문서의 출력 방식을 변경하세요.
