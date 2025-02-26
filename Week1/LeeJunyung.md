## 🇶 웹 API의 발전 과정에서 SOAP에서 REST로의 전환이 일어난 이유와 그 장단점에 대해 설명하세요.
#### 🌟SOAP (Simple Object Access Protocol) : 웹 서비스에서 기본적인 메시지를 전달하는 프로토콜
-> 웹 애플리케이션 간 데이터를 주고받을 수 있도록 설계되었으며, XML 기반의 메시지를 사용한다.
#### 🌟REST (Representational State Transfer) : 소프르퉤어 아키텍처 디자인의 한 스타일이며, 웹의 확장성과 상호 운용성을 높이기 위해 정의된 개념
특징 
- 효율적이고, 안정적이며 확장 가능한 분산시스템을 구현할 수 있다.
- HTTP 표준을 따르기 때문에 특정 언어나 기술에 종속되지 않고 모든 플랫폼에서 자유롭게 사용할 수 있다.
- 균일한 인터페이스를 기본으로 한다.

### 📌 SOAP에서 REST로 전환하는 이유
과거에는 SOAP가 웹 서비스 통신에서 널리 사용되었지만, 웹과 모바일 환경이 다양해지고 발전하면서, 보다 가볍고 유연한 아키텍처의 사용이 요구되었다. 
<br> 이에 따라 REST가 등장해 점차 SOAP를 대체하게 되었다. 
1. 경량성 : SOAP는 XML 기반으로 메세지가 크고 무거운 반면, REST는 JSON, XML 등 다양한 형식을 지원하며, 메시지 크기가 작아 네트워크 비용이 낮다.
2. 단순성 : REST는 HTTP프로토콜을 그대로 활용하고, URL과 HTTP Method(GET,POST,PUT,PATCH,DELETE) 를 이용해 직관적이며 이해하기 쉽다.
3. 확장성 : REST API는 클라이언트와 서버 간의 결합도를 낮추어 다양한 환경에서 쉽게 사용할 수 있다.
4. 캐싱 가능 : REST는 HTTP의 캐싱 기능을 활용할 수 있어 성능이 향상된다.
5. 표준 기술과의 호환성 : REST는 JSON과 같은 웹 친화적인 기술과 잘 어울리기 때문에 JavaScript 기반의 웹 애플리케이션등과 쉽게 연동할 수 있다는 장점을 가진다.

### 📌 SOAP vs REST의 장단점 비교
| 비교 항목       | SOAP                                     | REST                                   |
|---------------|--------------------------------------|--------------------------------------|
| **프로토콜**   | 자체 프로토콜(XML 기반)                    | HTTP 기반                              |
| **메시지 형식** | XML                                    | JSON, XML, YAML 등                     |
| **성능**       | 무겁고 복잡                               | 가볍고 빠름                             |
| **보안**       | WS-Security 지원 (높은 보안)              | HTTPS, OAuth 등 별도 구현 필요          |
| **트랜잭션 지원** | ACID 트랜잭션 지원                       | 기본적으로 지원하지 않음                   |
| **표준성**     | WSDL을 통한 명확한 인터페이스 정의          | RESTful 원칙을 따르지만, 명확한 표준은 없음 |
| **사용 사례**   | 엔터프라이즈 애플리케이션, 금융 서비스       | 웹, 모바일 API, 마이크로서비스           |

> 즉, REST는 웹 서비스와 클라우드 환경에서 주로 활용되고 있고, SOAP는 금융 및 기업용 애플리케이션에서 여전히 활용되고 있다.

## 🇶 Spring Boot에서 @RestController로 들어온 HTTP 요청이 처리되어 응답으로 변환되는 전체 과정을 설명하세요. 특히 HTTP 메시지 컨버터가 동작하는 시점과 역할을 포함해서 설명하세요.
### 📌 HTTP 요청 처리 단계 
1. 클라이언트 요청
   - 브라우저, postman, 모바일 앱 등의 클라이언트가 HTTP 요청을 전송한다.
   - ex. GET/users/1
2. 서블릿 컨테이너(Tomcat)에서 요청 수락
  - Spring Boot 내장 웹 서버(Tomcat, Jetty 등) 가 요청을 수신하고, DispatcherServlet에 전달
3. DispatcherServlet에서 컨트롤러 매핑
  - DispatcherServlet은 요청 URL과 @RequestMapping 또는 @GetMapping, @PostMapping 등의 애너테이션을 기반으로 컨트롤러 메소드를 찾는다
4. 컨트톨러에서 비즈니스 로직 실행
  - @RestController가 붙은 컨트롤러의 메소드가 실행됨
  - 서비스 계층을 호출하여 필요한 데이터를 가져옴
5. HTTP 메시지 컨버터(HttpMessageConverter) 동작
  - 컨트롤러의 반환 객체를 HTTP 응답으로 변환하는 과정에서 HttpMessageConverter 가 동작함
  - 일반적으로 MappingJackson2HttpMessageConverter 가 JSON 변환을 수행
  - produces = "application/json" 설정시 JSON 형식으로 변환됨
6. 응답을 DispatcherServlet이 받아 클라이언트에 전달함
  - 변환된 HTTP 응답을 DispatcherServlet이 받아 클라이언트에 반환

### 📌 HTTP 메시지 컨버터 (HttpMessageConverter)의 역할과 동작 시점
#### - 역할 : 컨트롤러에서 반환한 객체를 적절한 HTTP 응답 형식(JSON, XML 등)으로 변환한다. 
#### - 동작 시점 : 컨트롤러에서 응답 데이터를 반환할 때 DispatcherServlet이 이를 감지해 HttpMessageConverter를 호출한다.
##### 💠 예제 코드 
```
@RestController
@RequestMapping("/api/users")
public class UserController {
  private final UserService userService;

  public UserController(UserService userService) {
    this.userService = userService;
  }

  @GetMapping("/{id}")
  public ResponseEntity<UserDto> getUser(@PathVariable UUID id) {
    UserDto user = userService.getUserById(id);
    return ResponseEntity.ok(user);
  }
}
```
