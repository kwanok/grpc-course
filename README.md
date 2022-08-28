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
