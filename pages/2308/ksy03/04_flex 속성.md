# Flex box의 속성

#### flex container 속성

- flex-direction: 아이템 배치 축 방향 결정
- flex-wrap: 컨테이너의 아이템이 넘칠 경우의 줄바꿈
- flex-flow: `flex-direction`, `flex-wrap`
- justify-content: 메인축 방향으로 아이템 정렬
- align-items: 교차축 방향으로 아이템 정렬
- align-content: `flex-wrap: wrap`의 경우 교차축 방향 정렬

#### flex item 속성

- flex-basis: 아이템의 기본 크기 설정
- flex-grow: flex container 요소 내부 확장 비율
- flex-shrink: flex container 요소 내부 축소 비율
- flex: `flex-grow`, `flex-shrink`, `flex-basis`
- align-self: 교차축 방향의 해당 아이템 정렬
- order: 시각적 나열 순서

<style>
    h4 {
        @apply mt-2;
    }
    li {
        @apply text-[16px];
    }
</style>

---

# flex-direction

아이템 배치 축 방향 결정

<div grid="~ cols-2 gap-8">

<div>

<div class="flex">
    <div class="flex-item">flexItem</div>
    <div class="flex-item">flexItem</div>
    <div class="flex-item">flexItem</div>
    <div class="flex-item">flexItem</div>
</div>

<br>

<div class="flex flex-column">
    <div class="flex-item">flexItem</div>
    <div class="flex-item">flexItem</div>
    <div class="flex-item">flexItem</div>
    <div class="flex-item">flexItem</div>
</div>

</div>

<div>


```css
display: flex;
flex-direction: row;
```

<br>
<br>

```css
display: flex;
flex-direction: column;
```

</div>

</div>

<style>
    .flex {
        display: flex;
        background: #f0f0f0;
        padding: 20px 8px;
        gap: 8px;
    }
    .flex-column {
        flex-direction: column;
    }
    .flex-item {
        flex: 1;
        background-color: #62b37e;
        color: white;
        text-align: center;        
        line-height: 50px;
    }
</style>

---

# flex-wrap

항목이 전혀 줄어들 수 없거나 충분히 줄어들 수 없을 때 흘러넘침.

<div grid="~ cols-2 gap-8">

<div class="flex-col gap-4" style="display:flex;">

<div class="flex">
    <div class="flex-item">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
    <div class="flex-item">flexItem 4</div>
    <div class="flex-item">flexItem 5</div>
</div>

<div class="flex" style="flex-wrap: wrap;">
    <div class="flex-item">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
    <div class="flex-item">flexItem 4</div>
    <div class="flex-item">flexItem 5</div>
</div>

<div class="flex" style="flex-wrap: wrap-reverse;">
    <div class="flex-item">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
    <div class="flex-item">flexItem 4</div>
    <div class="flex-item">flexItem 5</div>
</div>


</div>

<div>

```css
display: flex;
flex-wrap: nowrap;
```

<div class="pb-10"></div>

```css
display: flex;
flex-wrap: wrap;
```

<div class="pb-20"></div>

```css
display: flex;
flex-wrap: wrap-reverse;
```

</div>

</div>

<style>
    .flex {
        display: flex;
        background: #f0f0f0;
        padding: 20px 8px;
        gap: 8px;
    }
    .flex-column {
        flex-direction: column;
    }
    .flex-item {
        white-space: nowrap;
        background-color: #62b37e;
        color: white;
        text-align: center;        
        line-height: 40px;
    }
</style>


---

# justify-content

---

# align-items

---

# align-content

---

# flex-basis

---

# flex-grow

---

# flex-shrink

---

# align-self

---

# order