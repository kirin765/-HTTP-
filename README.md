# 모든 개발자를 위한 HTTP 웹 기본 지식 정리

## 인터넷 통신
* 인터넷 상 수많은 노드를 통해 컴퓨터간 데이터가 전송된다.

## IP(인터넷 프로토콜)
* 출발지 IP, 목적지 IP 등이 담긴 IP 패킷
* 한계성 - 비연결성 : 패킷 대상 없거나 불능인데 전송함
* 한계성 - 비신뢰성 : 패킷 소실, 패킷 순서 확인 불가
* 한계성 - 프로그램 구분 : 같은 IP내 여러 프로그램 구분 불가

## TCP, UDP
* 프로토콜 계층 지나면서 TCP 패킷, IP 패킷 ... 이 겹겹이 쌓여간다.
* TCP 패킷 : 출발 PORT, 목적지 PORT, 전송제어, 순서, 검증 정보...
* TCP - 연결지향 : TCP 3 way handshake |  1. SYN 2. SYN+ACK 3. ACK
* TCP - 데이터 전달 보증 | 1. 데이터 전송 2. 데이터 잘 받았음 
* TCP - 순서 보장 | 1. 패킷 1, 2, 3 순서로 전송 2. 1, 3, 2로 도착 3. 2부터 다시 요청
* TCP - 신뢰할 수 있는 프로토콜
* UDP - 기능이 없다.
* UDP - TCP와 달리 애플리케이션 레벨에서 커스텀 가능
* UDP - 3 way handshake X, 전달 보증 X, 순서 보장 X -> 단순, 빠름
* UDP - IP에서 PORT, 체크섬만 추가

## PORT
* 같은 IP내 프로세스 구분 위함

## DNS
* 1. IP 주소 기억 어려움
* 2. IP 변경될 경우 통신 어려움
* 위 두가지 해결

## URI
* Uniform Resource Identifier
* 리소스 구분
* 1. URL (foo://example.com:8042/over/there?name=ferret#nose)  
* 2. URN (urn:example:animal:ferret:nose) 거의 사용 X
* scheme://[userinfo@]host[:port][/path][?query][#fragment]
* https://www.google.com:443/search?q=hello&hl=ko

## 웹 브라우저 요청 흐름
* 1. 웹 브라우저가 HTTP 메시지 생성
* 2. SOCKET 라이브러리를 통해 전달
* A. TCP/IP 연결(IP, PORT) 3 핸드 세이킹...
* 3. TCP/IP 패킷 생성, HTTP 메시지 포함

## 모든 것이 HTTP
* HTTP1.1, HTTP2, HTTP3(UDP)

## 클라이언트 서버 구조
* HTTP
* 양쪽이 구분되어 짐으로써 독립적인 개발이 가능해짐

## Stateful, Stateless
* Stateless는 Scale Out이 가능
* Stateless는 데이터를 많이 보낸다.

## 비 연결성(connectionless)
* HTTP 지속 연결(Persistent Connections)로 필요한 것 다 요청 후 연결 끊음
* 한 개 요청하고 끊고 다시 연결하고 끊고 반복시 느림

## HTTP 메시지
* start-line | header | message body

## HTTP API를 만들어보자
* 회원 목록 조회 /read-member-list -> /members
* 회원 조회 /read-member-by-id -> /members/{id}
* 리소스(회원), 행위(조회, 등록...) 구분
* 리소스는 URI로 구분

## HTTP 메서드 - GET, POST
* GET - 리소스 조회, 메시지 바디 없음
* POST - 다양한 데이터 처리, 메시지 바디 있음

## HTTP 메서드 - PUT, PATCH, DELETE
* PUT - 리소스를 완전히 갈아치움, 클라이언트가 명확히 리소스 지정
* PATCH - 일정부분만 변경

## HTTP 메서드의 속성
* 안전 - 호출해도 리소스 변경X, GET, HEAD
* 멱등 - 몇번 호출하든 같다. GET, PUT, DELETE
* 캐시가능 - GET, HEAD, POST, PATCH 가능, 주로 GET, HEAD

## 클라이언트에서 서버로 데이터 전송
* 정적 데이터 조회 - GET, 쿼리 파라미터
* 동적 데이터 조회 - HTML FORM, POST, GET, multipart form, x-www... urlencoded
* HTTP API 통신 - aplication/json

## HTTP API 설계 예시
* POST /members, 메시지 바디에 데이터 넣고 서버에 맡긴다. Collection방식
* PUT /files/star.jpg, 클라이언트가 상세히 알고있다. Store방식
* /new, /edit ... 컨트롤 URI - 동사가 표현, POST
* 문서, 컬렉션, 스토어, 컨트롤러(컨트롤 URI)

## HTTP 상태코드 소개
* 클라이언트 요청에 대해 처리상황을 응답으로 알려주는 것

## 2xx - 성공
* 200 OK, 201 Created, 202 Accepted, 204 No Content

## 3xx - 리다이렉션1
* 3xx 응답결과면 Location으로 이동
* 영구 리다이렉션, 일시 리다이렉션, 특수 리다이렉션
* 301 MovedPermanently GET 으로 재요청, 308 ...

## 3xx - 리다이렉션2
* 302 리다이렉트시 GET을 바뀔수도, 307 요청메서드 본문 유지, 303 GET으로 변경
* PRG - Post Redirect Get, 클라이언트 재요청시 POST로 다시 안 보내기 위함
* 304 Not Modified, 캐시를 위함

## 4xx - 클라이언트 오류, 5xx - 서버 오류
* 400 - 요청 구문, 메시지 오류
* 401 - 인증(Authentication) 되지 않음
* 403 - 접근 권한이 불충분 (Authorization)
* 404 - 요청 리소스가 서버에 없음
* 500 - 서버 내부 문제
* 503 - 일시적 장애, 복구시간 있음

## HTTP 헤더 개요
* HTTP 전송에 필요한 부가정보
* 표현헤더 + 표현 데이터(메시지 본문)

## 표현
* Content-Type, Content-Encoding, Content-Language, Content-Length

## 콘텐츠 협상
* 클라이언트가 선호하는 표현 요청
* Accept, ...-Charset, -Encoding, -Language
* en;q=0.9, ko;q=0.3

## 전송 방식
* Content-Length: 3423, 단순 전송
* Content-Encoding: gzip ..., 압축 전송
* Transfer-Encoding: chunked, 분할 전송
* Range: bytes=1001-2000 ->, <- Content-Range: bytes 1001-2000 / 2000, 범위 전송
