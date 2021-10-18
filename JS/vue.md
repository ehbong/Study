# VUE JS

* [Vue 공식문서](https://v3.vuejs.org/guide/introduction.html#what-is-vue-js)


```html
##### vue 시작하기
<!-- 개발버전, 도움되는 콘솔 경고를 포함. -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
또는:

<!-- 상용버전, 속도와 용량이 최적화됨. -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<div id="app">
  {{ message }}
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      message: '안녕하세요 Vue!'
    }
  })
</script>
```
