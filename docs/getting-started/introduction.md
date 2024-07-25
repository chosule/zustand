---
title: 소개
description: Zustand 사용방법
nav: 0
---

<div class="flex justify-center mb-4">
  <img src="https://github.com/pmndrs/zustand/raw/main/bear.jpg" />
</div>

Zustand는 작고 빠르며 확장 가능한 간편한 상태 관리 솔루션입니다. 
Zustand는 훅(hooks)을 기반으로 한 편리한 API를 제공하며, 복잡한 설정 없이도 사용할 수 있습니다. 
특정한 방식에 얽매이지 않으면서도 명확하고 flux와 같은 구조를 가지고 있습니다.

많은 시간을 들여 일반적인 문제들을 해결하였습니다. 예를들어, 악명 높은 [비정상적인 child 문제],
[React 동시성],그리고 혼합된 렌더링 사이의 [컨텍스트 손실] 같은 것들이 있습니다.
React에서 이러한 문제들을 모두 제대로 해결하는 상태 관리 라이브러리는 아마도 이게 유일할 것입니다.

demo를 실행해보세요[here](https://codesandbox.io/s/dazzling-moon-itop4).

[비정상적인 child 문제]: https://react-redux.js.org/api/hooks#stale-props-and-zombie-children
[React 동시성]: https://github.com/bvaughn/rfcs/blob/useMutableSource/text/0000-use-mutable-source.md
[컨텍스트 손실]: https://github.com/facebook/react/issues/13332

## 설치방법

Zustand는 NPM 패키지로 사용할 수 있습니다:

```bash
# NPM
npm install zustand
# Or, use any package manager of your choice.
```

## 먼저 store 생성하기

store는 훅(hook) 입니다.
원하는 것(원시값, 객체, 함수)을 모두 넣을수있습니다.
`set` 함수는 상태를 _병합(하나로 합쳐짐) 합니다._

```js
import { create } from 'zustand'

const useStore = create((set) => ({
  bears: 0,
  increasePopulation: () => set((state) => ({ bears: state.bears + 1 })),
  removeAllBears: () => set({ bears: 0 }),
  updateBears: (newBears) => set({ bears: newBears }),
}))
```

## 그런 다음 컴포넌트에 바인딩하고, 끝입니다!

providers 없이 어디에서나 훅(hook)을 사용할 수 있습니다.
상태를 선택하면 해당 상태를 사용하는 컴포넌트가 상태 변경 시 다시 렌더링 됩니다.

```jsx
function BearCounter() {
  const bears = useStore((state) => state.bears)
  return <h1>{bears} around here...</h1>
}

function Controls() {
  const increasePopulation = useStore((state) => state.increasePopulation)
  return <button onClick={increasePopulation}>one up</button>
}
```
