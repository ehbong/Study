# 네트워크

* [HTTP 동작과정](https://jess-m.tistory.com/17)
* [HTTPS에 대한 기초 이해](https://cheese10yun.github.io/https/)
* [Network 기초 유튜브강의](https://www.youtube.com/watch?v=k1gyh9BlOT8&list=PLXvgR_grOs1BFH-TuqFsfHqbh-gpMbFoy)
* [TCP 송/수신 원리](https://youtu.be/K9L9YZhEjC0)
* [TCP 동작원리 / 흐름제어](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=ksg7514&logNo=220772997742)
* [HTTP와 HTTPS 차이, SSL, TLS](https://beenii.tistory.com/83)
* [OSI 7layer 정리](https://jungeun960.tistory.com/181)
* [네트워크 기초 이론 유튜브](https://youtube.com/playlist?list=PLXvgR_grOs1BFH-TuqFsfHqbh-gpMbFoy)
* [L1, L2, L3, L4, L5, L6, L7 스위치란?](https://siahn95.tistory.com/entry/Network%EC%9E%A5%EB%B9%84-L1-L2-L3-L4-L5-L6-L7-%EC%8A%A4%EC%9C%84%EC%B9%98%EB%9E%80)
* [IP, Gateway, subnet에 대한 기본적인 이해](https://medium.com/pocs/tcp-ip-%EC%9D%B4%EB%A1%A0-ip-%EC%A3%BC%EC%86%8C-%EC%84%9C%EB%B8%8C%EB%84%B7-%EB%A7%88%EC%8A%A4%ED%81%AC-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EA%B8%B0%EB%B3%B8-%EA%B2%8C%EC%9D%B4%ED%8A%B8%EC%9B%A8%EC%9D%B4-ccd6d832711e)
* [TCP/IP 프로토콜과 패킷 교환 방식](https://better-together.tistory.com/110)
* [TCP/UDP 차이](https://velog.io/@hidaehyunlee/TCP-%EC%99%80-UDP-%EC%9D%98-%EC%B0%A8%EC%9D%B4)
* [TCP 연결과 해제](https://brunch.co.kr/@dreaminz/5)
* [TCP 제어플래그 종류](https://cezacx2.tistory.com/1256)
* [HTTP & HTTPS 패킷](https://velog.io/@fhwmqkfl/TILHTTP-HTTPS-%EA%B7%B8%EB%A6%AC%EA%B3%A0-Packet)
* [URL, URI, URN 차이](https://www.elancer.co.kr/blog/view?seq=74)
* [주 사용 port 번호 정리](https://ciscoking.tistory.com/12)
* [이메일 프로토콜 정리 SMTP, POP3, IMAP](https://post.naver.com/viewer/postView.naver?volumeNo=26957131&memberNo=2521903)
* [VPN 의 구조와 원리](https://www.youtube.com/watch?v=6w1F6qnPQiE&t=6s)
* [브라우저 동작원리](https://velog.io/@thyoondev/%EC%9B%B9-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%9D%98-%EB%8F%99%EC%9E%91%EC%9B%90%EB%A6%AC%EB%A5%BC-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)
* [DNS 동작원리 유튜브](https://youtu.be/6tqeANy-QoY)
* [도메인 네임 시스템 개념, 작동 방식](https://hanamon.kr/dns%EB%9E%80-%EB%8F%84%EB%A9%94%EC%9D%B8-%EB%84%A4%EC%9E%84-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EA%B0%9C%EB%85%90%EB%B6%80%ED%84%B0-%EC%9E%91%EB%8F%99-%EB%B0%A9%EC%8B%9D%EA%B9%8C%EC%A7%80/)
* [network socket](https://libertegrace.tistory.com/entry/Network-Socket-Programming)
* [CIDR에 대해](https://inpa.tistory.com/entry/WEB-%F0%9F%8C%90-CIDR-%EC%9D%B4-%EB%AC%B4%EC%96%BC-%EB%A7%90%ED%95%98%EB%8A%94%EA%B1%B0%EC%95%BC-%E2%87%9B-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC-%EA%B3%84%EC%82%B0%EB%B2%95#cidr_%EA%B3%84%EC%82%B0%EA%B8%B0)



> 브라우저에서 www.google.com 을 검색했을 때 동작 순서

1. 브라우저는 사용자가 입력한 URL인 "www.google.com"을 받아들입니다.
2. 브라우저는 이 URL을 해석하고, 해당 웹사이트의 IP 주소를 찾아야 합니다. 이를 위해 DNS(Domain Name System) 서버에 "www.google.com"이라는 호스트명에 대한 IP 주소를 요청합니다.
   이 전에 브라우저는 DNS캐시를 검색해서 캐시 정보를 확인하고 없으면 DNS서버에 요청합니다.
   (DNS 캐시는 유효기간이 존재, 유효기간은 DNS에 IP를 요청할 때 같이 받음)
2.1.   DNS 서버는 CNAME 레코드를 확인해서 CDN 정보가 있다면 해당 IP를 반환합니다.
3. 브라우저는 DNS 서버로부터 받은 IP 주소를 사용하여 해당 웹사이트의 서버와 TCP/IP 연결(3-way handshake)을 시도합니다. 이를 통해 브라우저는 해당 서버로 요청(request)을 보낼 수 있습니다.
4. 서버와의 연결이 성공적으로 이루어지면, 브라우저는 서버로부터 HTML, CSS, JavaScript 등의 웹 페이지 리소스를 요청합니다.
5. 서버는 이러한 리소스를 브라우저에 전송합니다.
6. 브라우저는 이 리소스를 받아 렌더링(화면에 표시)합니다.
7. 브라우저는 사용자가 요청한 페이지와 연관된 모든 리소스를 받을 때까지 이러한 단계를 반복합니다.
8. 최종적으로 사용자는 검색 페이지를 볼 수 있습니다.
