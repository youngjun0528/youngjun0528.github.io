# IoT 네트워크 프로그래밍

## HTTP
요청/응답(Request/Response) 패턴 기반
Client 가 Server 에 요청을 하면 Server 가 이에 응답을 하는 구성

## MQTT
게시/구독(Publish/Subscribe) 패턴 기반
HTTP 에 비해 경량화된 Header
- Publisher (게시자) : Message Broker 에 연결하여 콘텐츠를 전송한다.
- Subscriber (구독자) : Message Broker 에 연결하여 콘텐츠를 수신한다.
- Message Broker (메세지 중개자)

MQTT 를 게시/구독하는 모든 콘텐츠는 Topic (토픽) 을 통해 식별 관리된다.

QoS : MQTT 를 사용하여 게시할때 전송 Option
- 0 : 메세지를 한번만 전송한다. ( Fire on Forget )
- 1 : 메세지를 1회 전송건에 대해서 응답을 수신한다. 만약 Broker 가 응답을 수신하지 못하면 재발송하여 최소 한번은 전송한다.
- 2 : 메세지를 정확히 한번은 전송한다. Broker 가 응답을 수신하면 Publisher 에게도 응답값을 전송한다.

보안 관련 ( AWS IoT 사례 )
https://aws.amazon.com/ko/blogs/tech/mutual-tls-authentication-using-aws-iot-private-ca/
SSL/TLS ( TLS는 SSL의 업그레이드된 버전 - 고급 암호화 관리 )
- 초기 설정은 HTTPS 를 통해 서버와 통신을 하면 연결 구성을 시작한다.

- Device 에서 자체 생성한 PrivateKey 와 PublicKey 가 존재한다.
- 해당 Device 의 Public Key 로 서버에 MQTT 연결을 위한 인증서를 요청한다.
- 서버에서는 AWS IoT 와 함께 인증서를 확인하고 서명된 인증서를 생성한다. 
- AWS IoT 에서는 해당 Device 와 인증서를 매핑한다.
- 인증서가 정상적으로 발급되면 인증서와 접속 주소를 Device 로 전송한다.
- Device 는 발급된 인증서로 AWS IoT 에 Topic End-point 로 통신한다.


