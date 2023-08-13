# html, css

* [mdn doc](https://developer.mozilla.org/ko/docs/Learn)
* [CSS 공부의 방향성 feat figma](https://velog.io/@teo/CSS-%EA%B3%B5%EB%B6%80-%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%95%B4%EC%95%BC-%ED%95%98%EB%82%98%EC%9A%94-%EC%9D%B4%EB%A1%A0%ED%8E%B8-feat.-figma)

> 인라인, 블럭 요소

||inline|block|inline-block|
|---|---|---|---|
|기본너비|컨텐츠만큼|부모의 너비만큼|컨텐츠만큼|
|width, height 속성|무시|적용|적용|
|가로공간 차지|공유|독점|공유|
|margin 속성|가로만 적용|모두 적용(상하 상쇄)|모두 적용|
|padding 속성|가로만 적용, 세로는 배경색만|모두 적용|모두 적용|
|영역유지|컨텐츠의 형태로 변환|유지|유지|


### flex
> flex는 container 와 items로 구분  
> * container는 items를 감싸고 있는 부모
> * items는 각각의 객체

> container 속성  
> * display: flex 로 지정
> * flex-direction: 메인 축 방향
> * flex-wrap: 줄바꿈 처리 여부 및 방법
> * flex-flow: direction, wrap의 결합 속성, 같이 쓸 경우 direction, wrap 순서
> * justify-content: 메인 축의 정렬
> * align-items: 크로스 축의 단일 줄을 정렬, item들을 컨테이너 내에 정렬
> * align-content: 크로스 축의 여러 줄을 정렬 및 간격 조정

> items 속성  
> * order: 순서 지정(현재 기준 +,- 의 정수로 지정)
> * flex-grow: 아이템이 남는 공간을 차지하는 비율을 설정(다른 아이템과의 상대 길이)
> * flex-shrink: 아이템이 부족한 공간 내에 차지하는 비율을 설정(숫자가 크면 더 작아짐)
> * align-self: 개발 아이템의 크로스 축 정렬
