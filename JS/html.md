#HTML

> iframe 을 제한하는 방법
> 1. X-Frame-Options 사용
>    * DENY: 모든 iframe 내에 사용되지 않도록 차단
>    * SAMEORIGIN: 같은 출처(origin)일 때만 허용
>    * ALLOW-FROM <url>: 특정 URL에서만 허용 
```html
<!-- X-Frame-Options ALLOW-FROM <url> 예 -->
<meta http-equiv="X-Frame-Options" content="ALLOW-FROM https://allowed-domain.com">
```
> 2.CSP(Content Security Policy)
> * 서버측 응답 헤더 frame-ancestors 의 속성지정
> * meta태그 추가 
```html
<!-- meta태그 CSP 추가 예 -->
<meta http-equiv="Content-Security-Policy" content="frame-ancestors 'self';">
```
