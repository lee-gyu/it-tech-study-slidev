# Flex box의 구성요소

<div grid="~ cols-2 gap-4">

<div class="mr-20">
<arrow x1="60" y1="165" x2="440" y2="165" color="green" width="2" />
<arrow x1="410" y1="145" x2="410" y2="335" color="green" width="2" />
<div class="relative inline-flex bg-green-100 p-4 pt-9 h-40 gap-3 self-center mt-20 mb-2">
    <div class="absolute top-1 left-2">flex container</div>
    <div class="absolute -top-10 left-2 font-bold">main axis</div>
    <div class="absolute top-8 -right-10 font-bold"
        style="writing-mode: vertical-rl">cross axis</div>
    <div class="flex-item">flex item</div>
    <div class="flex-item">flex item</div>
    <div class="flex-item">flex item</div>
    <div class="flex-item">flex item</div>
</div>

```html
<div style="display: flex">
    <div>flex item</div>
    <div>flex item</div>
    <div>flex item</div>
    <div>flex item</div>
</div>
```

</div>

<div class="mt-10">
    <p><b>flex container</b><br>`display: flex`가 설정된 부모 요소</p>
    <p><b>flex item</b><br>flex container 내부 항목</p>
    <p><b>main axis(기본 축)</b><br> flex item이 배치되고 있는 방향으로 진행하는 수평 축</p>
    <p><b>cross axis(교차 축)</b><br> flex item이 배치되는 방향에 직각을 이루는 수직 축</p>    
</div>

</div>

<style>
    .flex-item {
        @apply bg-white
            p-2
            flex-1;
    }
</style>