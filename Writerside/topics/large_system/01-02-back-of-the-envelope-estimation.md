# 01.02 개략적인 규모 측정

## 서비스의 QPS 와 Storage Requirements

### 가정

1. 월간 능동 사용자는(Monthly Active User, MAU)는 300 million 명이다.
2. 50%의 사용자가 매일 서비스를 사용한다.
3. 평균적으로 각 사용자는 매일 2건씩 게시물을 등록한다.
4. 미디어를 포함하는 게시물을 10% 정도이다.
5. 데이터는 5년간 보관한다.

### 추정치

1. QPS(Query Per Seconds)
    - 일간 능동 사용자(Daily Active User, DAU) = MAU(300 million) * 50% = 150 million
    - QPS = DAU(150 million) * 2 / 24 / 60 / 60 = 3500
    - 최대 QPS (Peek QPS) : Peek Time 에 평균 QPS 에서 몇배를 할 것인지 결정 ( 2배, 4배, 8배 )
2. Storage Requirements
    - 게시물 ID (RDS 의 FLOAT Type) 으로 4 Byte
    - 날짜 : TIMESTAMP 값으로 4 Byte
    - 텍스트 : (최대 한글 200자 입력 가능 하다는 전제) 한글 1문자 2byte * 200 = 400 byte
    - 미디어 : 미디어 첨부파일은 1MB 로 제한
    - 하나의 게시물에 필요한 저장소 용량 = (Text : 4 + 4 + 400 ~= 400) + (Media : 1024 ~= 1000)
    - (150 million * 2){(400) + (0.1 * 1000)} = 150TB/D
    - 5년간 저장소 사이즈 = 150 * 365 * 5