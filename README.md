# Grpc Golang Course

## gRPC는 JSON보다 효율이 더 높다.

### 크기 차이

JSON 압축 해서 52 bytes 

```json
{
  "age": 26,
  "first_name": "Clement",
  "last_name": "JEAN"
}
```

gRPC 17 bytes

```protobuf
syntax = "proto3";

message Person {
  uint32 age = 1;
  string first_name = 2;
  string last_name = 3;
}
```

### 성능 차이

- JSON 파싱하는 과정에서 CPU 소모량이 많다
- JSON은 애초에 인간에 보기 쉬운 형태이다.
- gRPC는 이진 데이터를 읽어서 처리하기 때문에 성능이 더 높다.

## HTTP 1.0

- TCP 연결을 맺고, 요청을 보내고, 응답을 받고, 연결을 끊는다. 
- 여기서 문제는 마지막에 연결을 끊기 때문에 TCP 연결을 맺고 끊는 과정에서 오버헤드가 발생한다. 
- 헤더를 압축하지 않고 텍스트로 보내는데, 이는 네트워크에 부하를 준다. 
- 하나의 TCP 연결에 하나의 요청만 보낼 수 있다.

만약 클라이언트가 서버에 html, css, js 파일을 요청하려면

1. TCP 연결을 맺는다.
2. html 파일을 요청한다.
3. 서버가 html 파일을 보낸다.
4. TCP 연결을 끊는다.
5. TCP 연결을 맺는다.
6. css 파일을 요청한다.
7. 서버가 css 파일을 보낸다.
8. TCP 연결을 끊는다.
9. TCP 연결을 맺는다.
10. js 파일을 요청한다.
11. 서버가 js 파일을 보낸다.
12. TCP 연결을 끊는다.

이렇게 총 12개의 단계를 거쳐야 합니다.

## HTTP 2.0

- HTTP 1.0의 문제점을 보완하기 위해 나온 프로토콜
- 하나의 TCP 연결에 여러 요청을 보낼 수 있다.
- TCP 연결을 맺고 끊는 과정이 없다.
- 헤더를 압축해서 보낸다. (Binary Data)
- 서버 푸시 기능을 제공한다.
- 스트림을 제공한다.
- SSL/TLS를 사용한다.

만약 클라이언트가 서버에 html, css, js 파일을 요청하려면

1. TCP 연결을 맺는다.
2. html, css, js 파일을 요청한다.
3. 서버가 html, css, js 파일을 보낸다.
4. TCP 연결을 끊는다.

4 단계만으로 효율적으로 처리할 수 있습니다.