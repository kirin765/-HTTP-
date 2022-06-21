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

