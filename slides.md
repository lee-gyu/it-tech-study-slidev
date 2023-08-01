---
theme: seriph
background: none
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
title: 이노룰스 IT 기술 스터디
---

# 이노룰스 IT 기술 스터디 1기

Web, Java, AI 등 폭 넓은 IT 주제 스터디 모임

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    스터디 진행 목록 확인<carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/lee-gyu/it-tech-study-slidev" target="_blank" alt="GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: slide-up
---

# 1기 23.08.17 (목)

각자 선정한 스터디 학습 주제

- 📝 **이규철** - 룰 시스템 Configuration
- 🎨 **김도현** - React 상태 관리 (Context API, Recoil)
- 🧑‍💻 **김소윤** - CSS flex-box 레이아웃

---
src: ./pages/2308/lee-gyu/innorules.md
hide: false
---

---
src: ./pages/2308/kdh379/react-state-management.md
hide: false
---

---
src: ./pages/2308/ksy03/css-flex-box.md
hide: false
---

---
layout: center
class: text-center
---

# Refer. slidev

[Documentations](https://sli.dev) · [GitHub](https://github.com/slidevjs/slidev) · [Showcases](https://sli.dev/showcases.html)
