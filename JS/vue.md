# VUE JS

* [Vue 공식문서](https://v3.vuejs.org/guide/introduction.html#what-is-vue-js)
* [모질라 내 vue 설명](https://developer.mozilla.org/ko/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_getting_started)
* [vscode 익스텐션 추천](https://linked2ev.github.io/devsub/2020/08/31/Visual-Studio-Code-vue.js-%EA%B0%9C%EB%B0%9C%EC%8B%9C-%EC%B6%94%EC%B2%9C-plugin-%EC%A0%95%EB%A6%AC/)
* [vue 기본 기능 애플코딩 강의](https://www.youtube.com/watch?v=-tVaahsXpwk&list=PLfLgtT94nNq3Br68sEe26jkOqCPK_8UQ-)
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
> v-if 는 그릴지 안그릴지, v-show 는 css 속성만 변경
>> v-if 는 자주 바뀌지 않는 조건에, v-show는 자주 바뀌는 조건에 적용
