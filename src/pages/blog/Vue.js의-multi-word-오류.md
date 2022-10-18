---
layout: '../../layouts/PostLayout.astro'
title: 'Vue.js의 multi-word 오류'
description: 'error Component name "Generation" should always be multi-word. vue/multi-word-component-names'
pubDate: 'Oct 17 2022'
heroImage: '/Vue.js의-multi-word-오류/eslint-plugin-vue.png'
---

![스크린샷-2022-09-29-오전-11.06.47.png](/src/assets/Vue.js의-multi-word-오류/스크린샷-2022-09-29-오전-11.06.47.png)

Vue.js로 화면 개발을 할 때, 아래와 같은 오류가 나올 때가 있다.

```zsh
error Component name 'Generation' should always be multi-word
vue/multi-word-component-names
```

`eslint-plugin-vue`를 사용하기 때문에 발생한 오류다. 오류 내용을 보면 Component의 이름은 항상 여러 단어여야 한다고 한다.

[vue/multi-word-component-names](https://eslint.vuejs.org/rules/multi-word-component-names.html)여기서 규칙 내용을 보면 `App.vue`와 같이 Vue에서 제공하는 내장 구성 요소를 제외하고는 구성 요소의 이름이 항상 여러 단어여야 하고, 이는 모든 HTML 요소가 한 단어이기 때문에 기존 및 미래 HTML 요소와의 충돌을 방지하기 때문이다.

![스크린샷-2022-09-29-오전-11.07.46.png](/src/assets/Vue.js의-multi-word-오류/스크린샷-2022-09-29-오전-11.07.46.png)

![스크린샷-2022-09-29-오전-11.07.53.png](/src/assets/Vue.js의-multi-word-오류/스크린샷-2022-09-29-오전-11.07.53.png)

![스크린샷-2022-09-29-오전-11.07.18.png](/src/assets/Vue.js의-multi-word-오류/스크린샷-2022-09-29-오전-11.07.18.png)

`Generation`을 `SentenceGeneration` 으로 Component의 이름을 여러 단어 조합으로 바뀌주니 오류가 사라졌다.

규칙 세부 정보를 살짝보자면,

```zsh
/* ✓ GOOD */
Vue.component('todo-item', { // ... })

/* ✗ BAD */
Vue.component('Todo', { // ... })
```

```zsh
/* ✓ GOOD */
export default {
  name: 'TodoItem',
  // ...
}

/* ✗ BAD */
export default {
  name: 'Todo',
  // ...
}
```

물론 Component의 이름을 한 단어로만 하고 싶다면 아래 코드로 한 단어로 허용할 Component의 이름을 적어주면 된다.

```json
{
  "vue/multi-word-component-names": [
    "error",
    {
      "ignores": []
    }
  ]
}
```

허용할 Component의 이름을 적어주는게 귀찮고 전부 한 단어로 하고 싶다면, 완전히 꺼버리면 되는데 추천하지는 않는다.

```json
{
  "vue/multi-word-component-names": 0
}
```
