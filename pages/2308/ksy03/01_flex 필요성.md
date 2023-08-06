# Flex가 필요한 이유

<br>

<div class="flex w-full h-20 p-2 gap-x-2 border-1 border-gray-500 items-center">    
    <span>ID</span>
    <input class="flex-1 border-1 rounded-1">
    <button class="bg-blue-500 text-white px-2">로그인</button>
</div>

<br>

<div class="flex w-full h-30 p-2 border-1 border-gray-500
bg-gray-100">
    <span class="border-1 bg-red-100 flex-1">Content</span>
    <span class="border-1 bg-green-100 flex-1">Loooooooooooong content</span>
    <span class="border-1 text-[24px] bg-purple-100 flex-1">big font size</span>
</div>

<br>

### 구현하기 어려운 레이아웃
 -> `float`, `position`, `display`

<div v-click
    class="text-[50px] absolute bottom-20 left-85">
    <span class="text-red font-bold pr-5">X</span>
</div>
<div v-after class="flex fixed top-0 left-0 h-full w-full bg-black opacity-80 items-center justify-center">
    <span class="text-[50px] font-black text-white">Flex Box</span>
</div>
 