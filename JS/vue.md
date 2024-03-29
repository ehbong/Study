# VUE JS

* [Vue 공식문서](https://v3.vuejs.org/guide/introduction.html#what-is-vue-js)
* [Vue Cli 공식문서](https://cli.vuejs.org/guide/)
* [모질라 내 vue 설명](https://developer.mozilla.org/ko/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Vue_getting_started)
* [vue 핵심구조](https://brunch.co.kr/@clay1987/138)
* [vscode eslint 설정](https://velog.io/@skyepodium/VS-code%EC%97%90%EC%84%9C-vue%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-eslint-%EC%A0%81%EC%9A%A9-7xjr4r2on5)
* [emit](https://webruden.tistory.com/925)
* [vue websocket 재연결](https://www.wenyanet.com/opensource/ko/607968839d8f407d3d356859.html)
* [vscode 익스텐션 추천](https://linked2ev.github.io/devsub/2020/08/31/Visual-Studio-Code-vue.js-%EA%B0%9C%EB%B0%9C%EC%8B%9C-%EC%B6%94%EC%B2%9C-plugin-%EC%A0%95%EB%A6%AC/)
> 1. material icon theme
> 2. file icon theme
> 3. Vetur
> 4. Vue VSCode Snippets
> 5. night Owl
> 6. live server
> 7. ESLint
> 8. Prettier
> 9. Auto Close Tag
> 10. Atom Keymap
* [vue 기본 기능 애플코딩 강의](https://www.youtube.com/watch?v=-tVaahsXpwk&list=PLfLgtT94nNq3Br68sEe26jkOqCPK_8UQ-)
* [vue 크롬 디버깅](https://vuejs-kr.github.io/vue/2017/02/25/vue-chrome-debugging/)
> 크롬 디버깅 시 크롬 디버깅 브라우저에 vue 프론트 서버 띄운 것을 열어서 디버깅
* [vue vscode 디버깅](https://v3.ko.vuejs.org/cookbook/debugging-in-vscode.html#%E1%84%8B%E1%85%A1%E1%87%81%E1%84%89%E1%85%A5-%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%E1%84%92%E1%85%A1%E1%86%AF-%E1%84%80%E1%85%A5%E1%86%BA)
* [Component 활용](https://ux.stories.pe.kr/131)
```vue
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

* [Props & Emit 사용법](https://any-ting.tistory.com/41)

##### Invalid Host header 처리방법
```javascript
// filename : vue.config.js
module.exports = {
  // options...
  devServer: {
    disableHostCheck: true
  }
};
```
##### route 설치

```bash
  $ vue add router
```
* [lazy load(비동기 파일 요청)](https://kyounghwan01.github.io/blog/Vue/vue/lazy-loading/#%E1%84%8B%E1%85%B5%E1%84%80%E1%85%A5%E1%86%BA%E1%84%8B%E1%85%B3%E1%86%AF-%E1%84%92%E1%85%A1%E1%84%82%E1%85%B3%E1%86%AB-%E1%84%8B%E1%85%B5%E1%84%8B%E1%85%B2)
* [prefetch 설명](https://code-hoon.tistory.com/163)
```javascript
// prefetch 끄는방법
// vue.config.js 내에 작성
module.exports = {
  chainWebpack: config => {
    config.plugins.delete('prefectch'); // prefetch 삭제
  }
}
```
* [페이지 별 접근권한](https://minhanpark.github.io/today-i-learned/role-in-vuerouter/)
* [computed 와 watch 비교](https://kr.vuejs.org/v2/guide/computed.html)

##### Quasar
> vue.js기반 오픈소스 프레임워크
> * Material Design을 기본 지원
> * tree-shakable 를 통해 사용하지 않는 함수를 제거해 코드 최적화
> * 데스크톱 및 모바일 브라우저 환경 지원
> * SPA, SSR 등 각 빌드 모드 지원
* [Quasar 공식문서](https://quasar.dev/start/quick-start)
> 공식 문서 검색을 통해 grid, button 등 사용법을 검색해서 사용
* [vue 프로젝트 생성 및 기본 사용법](https://godffs.tistory.com/3306)


#### nuxtjs
* [nuxtjs공식](https://nuxtjs.org/)
