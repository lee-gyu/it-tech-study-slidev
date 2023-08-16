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

메인축 방향으로 아이템 정렬

<div grid="~ cols-2 gap-8">

<div class="flex-col gap-1" style="display:flex;">

<div class="flex" style="justify-content: flex-start">
    <div class="flex-item">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>
<div class="flex" style="justify-content: flex-end">
    <div class="flex-item">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>
<div class="flex" style="justify-content: center">
    <div class="flex-item">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>
<div class="flex" style="justify-content: space-between">
    <div class="flex-item">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>
<div class="flex" style="justify-content: space-around">
    <div class="flex-item">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>
<div class="flex" style="justify-content: space-evenly">
    <div class="flex-item">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>

</div>

<div>

```css
display: flex;
justify-content: flex-start;
```

<div class="pb-1"></div>

```css
display: flex;
justify-content: flex-end;
```

<div class="pb-1"></div>

```css
display: flex;
justify-content: center;
```
<div class="pb-2"></div>

```css
display: flex;
justify-content: space-between;
```
<div class="pb-2"></div>

```css
display: flex;
justify-content: space-around;
```
<div class="pb-2"></div>

```css
display: flex;
justify-content: space-evenly;
```

</div>

</div>

<style>
    .flex {
        display: flex;
        background: #f0f0f0;
        padding: 12px 8px;
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

# align-items

교차축 방향으로 아이템 정렬

<div grid="~ cols-2 gap-8">

<div class="flex-col gap-1" style="display:flex;">

<div class="flex" style="align-items: stretch">
    <div class="flex-item" style="font-size: 12px">flexItem 1</div>
    <div class="flex-item" style="font-size: 26px">flexItem 2</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
</div>
<div class="flex" style="align-items: flex-start">
    <div class="flex-item" style="font-size: 12px">flexItem 1</div>
    <div class="flex-item" style="font-size: 26px">flexItem 2</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
</div>
<div class="flex" style="align-items: flex-end">
    <div class="flex-item" style="font-size: 12px">flexItem 1</div>
    <div class="flex-item" style="font-size: 26px">flexItem 2</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
</div>
<div class="flex" style="align-items: center">
    <div class="flex-item" style="font-size: 12px">flexItem 1</div>
    <div class="flex-item" style="font-size: 26px">flexItem 2</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
</div>
<div class="flex" style="align-items: baseline">
    <div class="flex-item" style="font-size: 12px">flexItem 1</div>
    <div class="flex-item" style="font-size: 26px">flexItem 2</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
</div>

</div>

<div>

```css
display: flex;
align-items: stretch;
```

<div class="pb-1"></div>

```css
display: flex;
align-items: flex-start;
```

<div class="pb-1"></div>

```css
display: flex;
align-items: flex-end;
```
<div class="pb-2"></div>

```css
display: flex;
align-items: center;
```
<div class="pb-2"></div>

```css
display: flex;
align-items: baseline;
```
<div class="pb-2"></div>

</div>

</div>

<style>
    .flex {
        display: flex;
        background: #f0f0f0;
        padding: 12px 8px;
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
    }
</style>

---

# align-content

`flex-wrap: wrap`의 경우 교차축 방향 정렬

<div grid="~ cols-2 gap-8 items-center relative">

<div>

<div class="flex" style="flex-wrap: wrap;height: 300px;align-content: flex-start;">
    <div class="flex-item" style="font-size: 12px">flexItem 1</div>
    <div class="flex-item" style="font-size: 26px">flexItem 2</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
</div>

<div v-click="1" class="flex" style="flex-wrap: wrap;height: 300px;align-content: flex-end;">
    <div class="flex-item" style="font-size: 12px">flexItem 1</div>
    <div class="flex-item" style="font-size: 26px">flexItem 2</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
</div>
<div v-click="2" class="flex" style="flex-wrap: wrap;height: 300px;align-content: center;">
    <div class="flex-item" style="font-size: 12px">flexItem 1</div>
    <div class="flex-item" style="font-size: 26px">flexItem 2</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
</div>
<div v-click="3" class="flex" style="flex-wrap: wrap;height: 300px;align-content: space-between;">
    <div class="flex-item" style="font-size: 12px">flexItem 1</div>
    <div class="flex-item" style="font-size: 26px">flexItem 2</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
</div>
<div v-click="4" class="flex" style="flex-wrap: wrap;height: 300px;align-content: space-around;">
    <div class="flex-item" style="font-size: 12px">flexItem 1</div>
    <div class="flex-item" style="font-size: 26px">flexItem 2</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
</div>
<div v-click="5" class="flex" style="flex-wrap: wrap;height: 300px;align-content: space-evenly;">
    <div class="flex-item" style="font-size: 12px">flexItem 1</div>
    <div class="flex-item" style="font-size: 26px">flexItem 2</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
    <div class="flex-item" style="font-size: 20px">flexItem 3</div>
</div>

</div>

<div>

<div class="code">

```css
display: flex;
align-content: flex-start;
```

</div>

<div v-after="1" class="code">

```css
display: flex;
align-content: flex-end;
```

</div>
<div v-after="2" class="code">

```css
display: flex;
align-content: center;
```

</div>
<div v-after="3" class="code">

```css
display: flex;
align-content: space-between;
```

</div>
<div v-after="4" class="code">

```css
display: flex;
align-content: space-around;
```

</div>
<div v-after="5" class="code">

```css
display: flex;
align-content: space-evenly;
```

</div>

</div>

</div>


<style>
    .flex {
        position: absolute;
        top: 150px;
        width: 400px;
        display: flex;
        background: #f0f0f0;
        padding: 12px 8px;
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
    }
    .code {
        margin-top: 120px;
        position: absolute;
        width: 400px;
    }
</style>

---

# flex-basis

flex item의 초기 크기를 지정\
flex-basis와 width/height를 동시에 적용한 경우 flex-basis 우선 적용

<br>
<br>

<div grid="~ cols-2 gap-8">

<div class="flex-col gap-1" style="display:flex;">

<div class="flex">
    <div class="flex-item" style="flex-basis: auto">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>
<div class="flex">
    <div class="flex-item" style="flex-basis: 0">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>
<div class="flex">
    <div class="flex-item" style="flex-basis: 200px">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>

</div>

<div>

```css
flex-basis: auto;
```

<div class="pb-5"></div>

```css
flex-basis: 0;
```

<div class="pb-6"></div>

```css
flex-basis: 200px;
```

</div>

</div>

<style>
    .flex {
        display: flex;
        background: #f0f0f0;
        padding: 12px 8px;
        gap: 8px;
    }
    .flex-column {
        flex-direction: column;
    }
    .flex-item {
        box-sizing: content-box;
        white-space: nowrap;
        background-color: #62b37e;
        color: white;
        text-align: center;
        line-height: 40px;
    }
</style>

---

# flex-grow

flex item 요소가 flex-container 요소 내부에서 할당 가능한 공간 정도

<br>
<br>

<div grid="~ cols-2 gap-8">

<div class="flex-col gap-1" style="display:flex;">

<div class="flex">
    <div class="flex-item" style="flex-grow: 1">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>
<div class="flex">
    <div class="flex-item" style="flex-grow: 2">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>
<div class="flex">
    <div class="flex-item" style="flex-grow: 3">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>

</div>

<div>

```css
flex-grow: 1;
```

<div class="pb-5"></div>

```css
flex-grow: 2;
```

<div class="pb-6"></div>

```css
flex-grow: 3;
```

</div>

</div>

<style>
    .flex {
        display: flex;
        background: #f0f0f0;
        padding: 12px 8px;
        gap: 8px;
    }
    .flex-column {
        flex-direction: column;
    }
    .flex-item {
        flex: 1;
        box-sizing: content-box;
        white-space: nowrap;
        background-color: #62b37e;
        color: white;
        text-align: center;
        line-height: 40px;
    }
</style>

---

# flex-shrink

설정된 숫자값에 따라 flex-container 요소 내부에서 flex-item 요소의 크기가 축소

<br>
<br>

<div grid="~ cols-2 gap-8">

<div class="flex-col gap-1" style="display:flex;">

<div class="flex">
    <div class="flex-item" style="flex-shrink: 0">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>
<div class="flex">
    <div class="flex-item" style="flex-shrink: 1">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>
<div class="flex">
    <div class="flex-item" style="flex-shrink: 2">flexItem 1</div>
    <div class="flex-item">flexItem 2</div>
    <div class="flex-item">flexItem 3</div>
</div>

</div>

<div>

```css
flex-shrink: 0;
```

<div class="pb-5"></div>

```css
flex-shrink: 1;
```

<div class="pb-6"></div>

```css
flex-shrink: 2;
```

</div>

</div>

<style>
    .flex {
        display: flex;
        background: #f0f0f0;
        padding: 12px 8px;
        gap: 8px;
    }
    .flex-column {
        flex-direction: column;
    }
    .flex-item {
        flex: 1 1 200px;
        box-sizing: content-box;
        white-space: nowrap;
        background-color: #62b37e;
        color: white;
        text-align: center;
        line-height: 40px;
    }
</style>

---

# align-self

flex-item 수직축 방향 정렬

<br>
<br>

<div grid="~ cols-2 gap-8">

<div class="flex-col gap-1" style="display:flex;">

<div class="flex">
    <div class="flex-item">flexItem 1</div>
    <div class="flex-item" style="align-self: flex-start">flexItem 2</div>
    <div class="flex-item" style="align-self: flex-end">flexItem 3</div>
    <div class="flex-item" style="align-self: center">flexItem 4</div>
    <div class="flex-item" style="align-self: baseline">flexItem 5</div>
</div>

</div>

<div>

```css
align-self: auto;
/* align-self: stretch; */
/* align-self: flex-start; */
/* align-self: flex-end; */
/* align-self: center; */
/* align-self: baseline; */
```

</div>

</div>

<style>
    .flex {
        display: flex;        
        background: #f0f0f0;
        padding: 12px 8px;
        gap: 8px;
        height: 200px;
    }
    .flex-item {
        font-size: 14px;
        flex: 1 1 200px;
        box-sizing: content-box;
        white-space: nowrap;
        background-color: #62b37e;
        color: white;
        text-align: center;
    }
</style>