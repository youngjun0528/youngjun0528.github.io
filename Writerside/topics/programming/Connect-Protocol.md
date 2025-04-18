# 통신 프로토콜

1. 요청/응답(Request/Response) 패턴
대표적으로 HTTP 통신이 있다.
요청과 응답이 하나의 connection 내에서 이루어 진다.

서버에서 응답을 받기 위해서는 Waiting time 이 반드시 필요하다.

- 해결 방안
  - 반 비동기 : Client/Server 에서 비동기로 요청하는 방법
    - Client 는 서버로 요청을 날리고 응답이 오기까지 다른 일을 수행한다.
    - Server 는 Client 로부터 요청을 수신하고 각 수신된 요청을 비동기 방식으로 수행한다.
  - 완전 비동기 : Client/Server 는 서로간의 비동기로 요청을 처리한다.

2. 게시/구독(Publish/Subscribe) 패턴 기반
대표적으로 MQTT 통신이 있다.
   - Producer 가 Broker 에게 메세지를 전달한다.
   - 메세지는 Topic 으로 구분되어 전송된다.
   - Consumer 는 Topic 에 수신된 메세지를 가져온다.
   - 네트워크 상황에 따라 Queue 에 쌓인 메세지를 수신 처리한다.

HTTP 에 비해 경량화된 Header

QoS : MQTT 를 사용하여 게시할때 전송 Option
- 0 : 메세지를 한번만 전송한다. ( Fire on Forget )
- 1 : 메세지를 1회 전송건에 대해서 응답을 수신한다. 만약 Broker 가 응답을 수신하지 못하면 재발송하여 최소 한번은 전송한다.
- 2 : 메세지를 정확히 한번은 전송한다. Broker 가 응답을 수신하면 Publisher 에게도 응답값을 전송한다.

보안 관련 ( AWS IoT 사례 )
https://aws.amazon.com/ko/blogs/tech/mutual-tls-authentication-using-aws-iot-private-ca/
SSL/TLS ( TLS는 SSL의 업그레이드된 버전 - 고급 암호화 관리 )
- Device 에서 자체 생성한 PrivateKey 와 PublicKey 가 존재한다.
- 해당 Device 의 Public Key 로 서버에 MQTT 연결을 위한 인증서를 요청한다.
- 서버에서는 AWS IoT 와 함께 인증서를 확인하고 서명된 인증서를 생성한다.
- AWS IoT 에서는 해당 Device 와 인증서를 매핑한다.
- 인증서가 정상적으로 발급되면 인증서와 접속 주소를 Device 로 전송한다.
- Device 는 발급된 인증서로 AWS IoT 에 Topic End-point 로 통신한다.

일방향 암호화
양방향 암호화는 공개키와 개인키를 가지고 client 와 Server 간의 인증을 처리한다.
대칭키를 사용한다면 Client와 SErver 는 동일한 키를 가지고 암호화를 진행한다.

일방향 암호화는 Hash 함수를 사용하여 특정 Key 가 없이는 복호화가 불가능하게 한다.
