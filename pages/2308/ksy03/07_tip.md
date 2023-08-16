# Tip!

1. flexbox로 반응형 처리하기

<div class="grid grid-cols-[500px_auto] gap-x-sm items-center">

<img src="https://blog.kakaocdn.net/dn/2iJDe/btqON8W0QMd/haMA3VNH71rwhCXHYe0ryk/img.gif" srcset="https://blog.kakaocdn.net/dn/2iJDe/btqON8W0QMd/haMA3VNH71rwhCXHYe0ryk/img.gif" data-filename="flexlayout6.gif" data-origin-width="1182" data-origin-height="450" data-ke-mobilestyle="widthContent" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';">

```css
.flexbox{
    display: flex;
    flex-wrap: wrap;
}
.item{
    min-height: 150px;
    flex: 23% /* 4개의 컬럼 */
     /* flex-basis: 23%;
        flex-shrink: 1;
        flex-grow: 1; */
}
@media screen and (max-width:1023px){
    .item{
        flex-basis: 49%; /* 2개의 컬럼 */
    }
}
@media screen and (max-width:767px){
    .item{
        flex-basis: 100%; /* 1개의 컬럼 */
    }
}
```

</div>

---

2. 가변적인 자식 요소의 크기가 부모 요소보다 클 경우

부모 요소에 overflow를 적용이 안된다는 것은 자식 요소의 크기가 제한이 되지 않아서 발생

- `min-width: auto`가 flexItem 기본값인데 `flex-basis: auto`보다 우선적으로 적용
- `min-widht: 0`을 적용할 경우 `flex-basis: auto`가 우선 적용되어 아이템이 컨테이너에 들어감
  - "flex item이 container 밖으로 튀어 나가고 있다고 인식"

<br>

<div class="grid grid-cols-[500px_auto] items-center" >

<div class="flex bg-green-100 p-4 gap-x-2" style="width: 300px">
    <div class="bg-white">flexItem</div>
    <div class="flex-1 bg-white">
        <div class="truncate">flexItemflexItemflexItemflexItemflexItem</div>
    </div>
</div>

```css
.col-2{
  flex: 1;
}

.col-2 div {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
```

</div>

<div class="grid grid-cols-[500px_auto] items-center" >

<div class="flex bg-green-100 p-4 gap-x-2" style="width: 300px">
    <div class="bg-white">flexItem</div>
    <div class="flex-1 bg-white" style="min-width: 0">
        <div class="truncate">flexItemflexItemflexItemflexItemflexItem</div>
    </div>
</div>

```css
.col-2{
  flex: 1;
  min-width: 0;
}
```

</div>