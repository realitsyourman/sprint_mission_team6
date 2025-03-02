# Weekly paper 7

## 1. 웹 API의 발전 과정에서 SOAP에서 REST로의 전환이 일어난 이유와 그 장단점에 대해 설명하세요.

SOAP는 XML기반 메세지를 교환하는 프로토콜이다. 보안이나 메세지 전송에 많은 표준이 정해져 있기 때문에 복잡하다. 트랜잭션을 지원하기 때문에 은행 앱과 같은 경우에는 더 나은 선택이 될 수 있다.

REST API는 HTTP 프로토콜을 기반으로 하는 아키텍쳐 스타일이다. 데이터 포맷으로는 주로 JSON을 사용한다. HTTP와 JSON을 사용하기 때문에 SOAP에 비해 단순하고 웹 환경에 최적화되어 있다.

## 2. Spring Boot에서 @RestController로 들어온 HTTP 요청이 처리되어 응답으로 변환되는 전체 과정을 설명하세요. 특히 HTTP 메시지 컨버터가 동작하는 시점과 역할을 포함해서 설명하세요.

1. Dispathcer servlet이 요청을 받음
2. 해당 요청을 처리할 수 있는 handler와, 그 handler를 실행시킬 수 있도록 하는 handler adapter 를 찾음
   - 주로 어노테이션 기반의 RequestMappingHandlerAdapter 사용
3. handler adapter가 ArgumentResolver를 실행
4. ArgumentResolver가 컨트롤러가 필요로 하는 파라미터들을 생성
   - 각 요청 데이터들을 어노테이션에 맞게 변환해서 생성함
   - @RequestBody인 경우, ArgumentResolver 내부에서 HttpMessageConverter가 작동해서 JSON 데이터를 객체로 변환
5. handler adapter가 handler(controller) 실행
6. 응답 데이터는 ReturnValueHandler가 HttpMessageConverter를 사용해서 객체를 JSON으로 변환
