# 1. 웹 API의 발전 과정에서 SOAP에서 REST로의 전환이 일어난 이유와 그 장단점에 대해 설명하세요.
SOAP는 Simple Object Access Protocol의 줄임말이다. 그러나 이름과 다르게 SOAP는 서비스 간 통신 방법이 간단하지 않았다.

## SOAP 요청
```
<soap:Envelope 
    xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
    xmlns:ns="http://example.com/stockquote">
    <soap:Header>
        <ns:Token>abc123token</ns:Token>
    </soap:Header>
    <soap:Body>
        <ns:GetStockPrice>
            <ns:StockSymbol>GOOG</ns:StockSymbol>
        </ns:GetStockPrice>
    </soap:Body>
</soap:Envelope>
```
## SOAP 응답
```
<soap:Envelope 
    xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
    xmlns:ns="http://example.com/stockquote">
    <soap:Header>
        <ns:ServerTime>2024-02-24T10:30:00Z</ns:ServerTime>
    </soap:Header>
    <soap:Body>
        <ns:GetStockPriceResponse>
            <ns:Price>2850.50</ns:Price>
            <ns:Currency>USD</ns:Currency>
            <ns:LastUpdate>2024-02-24T10:29:55Z</ns:LastUpdate>
        </ns:GetStockPriceResponse>
    </soap:Body>
</soap:Envelope>
```
이러한 SOAP 데이터는 데이터 타입을 엄격하게 검사한다는 장점이 있지만,
XML 기반으로 작성되었기 때문에 단순하지 않고 복잡한 구조의 큰 데이터가 오고 가야했다.
이러한 과정에서 REST 방식의 통신 방법이 제시되었다.

---
# 2.  Spring Boot에서 @RestController로 들어온 HTTP 요청이 처리되어 응답으로 변환되는 전체 과정을 설명하세요. 특히 HTTP 메시지 컨버터가 동작하는 시점과 역할을 포함해서 설명하세요.
## 2.1 전체적인 흐름
1. 클라이언트의 요청이 `DispatcherServlet`으로 들어온다.
2. `DispatcherSevlet`은 사용자의 요청이 어떤 핸들러에 의해 매핑되어야 하는지 `HandlerMapping`을 통해 찾는다.
3. 핸들러 매핑을 찾게 되면 이제 그 핸들러 매핑에 맞는 `HandlerAdapter`를 찾는다.
4. `HandlerAapter`는 `handle()`을 통해 실제 로직을 실행하게 된다.

## 2.2 HttpMessageConvert는 어디서 작동하는가?
1. `HandlerAdapter`에서 실제 핸들러를 동작하기 전에 `ArgumentResolver`를 거치게 된다.
2. `ArgumentResolver`는 사용자가 요청한 데이터를 컨트롤러에서 받고 이걸 어떻게 처리해야할지 판단하여 객체로 변환하여 바꿔준다.
3. 이때 `ArgumentResolver` 안에 `HttpMessageConvert`가 작동한다.
4. 만약 사용자의 요청이 Json 형식으로 들어오면 Json을 처리할 수 있는 `HttpMessageConvert`가 동작하여 Json 요청 데이터를 객체로 변환해주는 것이다. (`MappingJackson2HttpMessageConverter`)
