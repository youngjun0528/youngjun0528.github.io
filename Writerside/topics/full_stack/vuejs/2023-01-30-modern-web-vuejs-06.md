# 06. Directive(지시자)

## v-if

```HAML
<p v-if="seen">이제 나를 볼 수 있어요</p>
<p v-if="!seen">이제 나를 볼 수 없어요</p>
<p v-else>이제 나를 볼 수 없어요</p>
<p v-else-if="neverSeen">이제 나를 볼 수 없어요</p>
```

## v-show

```HAML
<p v-show="seen">이제 나를 볼 수 있어요</p>
<p v-show="!seen">이제 나를 볼 수 없어요</p>
```

* v-if와 v-show 의 차이점
  v-if로 선언시 DOM 객체 자체가 아예 SHOW & DELETE 관계라면,
  v-show 선언시 DOM 객체는 SHOW & HIDE 관계이다.
  만약 숨겨진 DOM 객체에 대한 참조가 필요할 때, show 로 숨기기 처리만 하면 된다.

## v-bind

```HAML
<a v-bind:href="url">링크 이동 </a>
<img v-bind:src="imagePath"/>
<a :href="url">링크 이동 </a>
<img :src="imagePath"/>
```

```JSP
<template>
    <div class="hello">
        <h1>{{ msg }}</h1>

        <p v-if="seen">보인다</p>
        <p v-else>보이지 않는다</p>

        <p v-show="seen">Show</p>
        <p v-show="!seen">Not Show</p>

        <a v-bind:href="url">링크 이동 </a>

    </div>
</template>

<script>
    export default {
      name: "HelloWorld",
      data() {
        return {
          msg: "반갑습니다!",
          seen: false,
          url: 'http://google.com'
        };
      },
    };
</script>
```
