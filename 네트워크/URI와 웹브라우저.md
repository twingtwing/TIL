# URI와 웹브라우저 요청 흐름

## URI
### URI(Uniform Resource Identifier)
: URI는 로케이터(locator), 이름(name) 또는 둘 다 추가로 분류 될 수 있음  

> URI안에 [ URL(위치),URN(이름) ]이 존재함

URI 단어 뜻
- Uniform : 리소스 식별 하는 통일된 방식
- Resource : 자원, URI로 식별할 수 있는 모든 것(제한 없음)
- Identifier : 다른 항목과 구분하는데 필요한 정보

URL, URN 단어 뜻 
- URL - Locator : 리소스가 있는 위치를 지정
- URN - Name : 리소스에 이름 부여
- 위치는 변할 수 있지만, 이름은 변하지 않는다.  
- URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음

URL과  URI의 차이는 ?

URL 전체 문법
> scheme://[ userinfo@ ]host:[:port][/path][?query][#fragment]
 https://www.google.com/search?q=??

- 프로토콜(https)
- 호스트명(www.google.com)
- 포트번호(:80)
- 패스(/search)
- 쿼리 파라미터(q=??)

1. scheme
- 주로 프로토콜 사용
- 프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙 ex,http,https,ftp등등
- http는 80포트, https는 443포트 주로 사용, 포트는 거의 생략
- https는 http에 보안 추가 (HTTP Secure)

2.  userinfo
- URL에 사용자 정보를 포함해서 인증
- 거의 사용하지 않음

3. host
- 호스트 명
- 도메인 명 또는 IP주소를 직접 사용 가능

4. path
- 리소스 경로(path), 계층적 구조 (exm /member/VIP)

5.query
- key = value 형태
- ?로 시작, &로 추가 가능
- query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자형태 

6.fragment
- html 내부 북마크 등에 사용
- 서버에 전송하는 정보는 아님

## 웹브라우저 요청 흐름

1. DNS 조회 (scheme,prot 생략) -> IP와 포트 정보를 찾음
2. 웹브라우저에서 HTTP 요청 메세지 생성  
=> HTTP 요청메세지 형태
GET /path?key=value HTTP/1.1  
Host : www.google.com
3. Socket라이브러리를 통해 TCP/IP계층으로 연결, 데이터 전달
4. TCP/IP 패킷 생성, HTTP 메세지 포함
5. 요청 패킷로 전달
6. 서버가 HTTP 요청 메세지를 해석
7. 서버가 HTTP 응답 메세지를 전송(html형태)
8. 웹브라우저 HTML 렌더링