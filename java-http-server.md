# Java HTTP Server

NIO 란?

Non-blocking I/O 라고 부르고 New I/O라고 부르기도함

사전적인 정의로는 작업에 필요한 API 모음이라고도 한다.

코드 예제

```
private void run() throws IOException {
    //1.Listener
    InetSocketAddress address = new InetSocketAddress(8081);
    HttpServer httpServer = HttpServer.create(address,0);

    // Handler를 람다식으로 쓰자
    // 컨트롤러 같이 패스를 설정해준 느낌이라 생각하자
    httpServer.createContext("/", exchange -> {
        // 아무것도 없이 나오면 터미널에서 아~무것도 나오지 않음.

        // 1. Request
        displayRequest(exchange);
        // 2. Response

        String content = "Hello World!\n";
        sendContent(exchange,content);
    });

    httpServer.createContext("/hi", exchange -> {
        String content = "hi Parrots!!\n";
        sendContent(exchange, content);
    });

    httpServer.start();
}


//request 를 보여주는 method

private void displayRequest(HttpExchange exchange) throws IOException {
    String method = exchange.getRequestMethod();
    System.out.println("METHOD :::::"+method);
    URI uri = exchange.getRequestURI();
    String path = uri.getPath();
    System.out.println("PATH ::::  "+path);

    Headers headers = exchange.getRequestHeaders();
    for (String key : headers.keySet()) {
        List<String> va = headers.get(key);
        System.out.println(key);
    }

    InputStream inputStream = exchange.getRequestBody();
    //byte[] bytes = inputStream.readAllBytes();
    //String body = new String(bytes);
    // body에 넣는다면 출력될것이다

    // 이번 강의에는 responsebody를 위해 이방식으로 사용함.
    String body = new String(inputStream.readAllBytes());
    System.out.println(body);
}

//content 전송 method

private void sendContent(HttpExchange exchange, String content) throws IOException {

    byte[] bytes = content.getBytes();

    exchange.sendResponseHeaders(200, bytes.length);
    OutputStream outputStream = exchange.getResponseBody();
    outputStream.write(bytes);
    outputStream.flush();
}
```



후기 : 오늘은 메소드 분리 하면서 코딩을 하면서 메소드 분리를 통해 가독성을 늘리면서 재활용성까지 챙길수 있겠다 싶은 생각이 들엇다. 추가로 람다의 편안함도..

