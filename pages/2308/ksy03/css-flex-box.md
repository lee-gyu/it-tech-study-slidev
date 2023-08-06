---
layout: cover
background: none
---

# Flex box

### 기반기술팀 김소윤 사원

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---
transition: fade-out
---

# **Index**

- **소개** - flex box의 개념과 목적, 왜 필요한가?
- **기본 구성 요소** - Flex Container와 Flex Items
- **주요 속성** - flex 속성과 flex와 inline-flex의 차이점
- **예제** - 실제 웹 사이트 Flex box 활용 사례
- **팁** - Flex box 효과적으로 활용하고, 흔히 발생하는 문제와 해결방법

<br>
<br>

출처: [MDN - Flex box](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Flexbox)

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

<!--
Here is another comment.
-->

---
src: "./01_flex 필요성.md"
---

---
src: "./02_flex 정의.md"
---

---
src: "./03_flex 구성 요소.md"
---

---
src: "./04_flex 속성.md"
---

---
src: "./05_inline-flex.md"
---

---
src: "./06_예제.md"
---