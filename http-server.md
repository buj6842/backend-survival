---
description: HTTP SERVER 예제
---

# HTTP SERVER

```
private void run() throws IOException {
    // 1. Listen
    // (로컬에서 쓸 8080 포트로 열자)
    //강의는 8080이지만 현재 내 pc에서 8080포트로 쓰는 서버가잇어서 8081로 적용하였음
    ServerSocket listener = new ServerSocket(8081, 0);
    System.out.println("Listen !!");

    //응답한번 주면 끝나니까 테스트를위해 무한루프로 변경
    while (true) {

        // 2. Accept
        Socket socket = listener.accept();

        System.out.println("Accept!");
        // 3. Request -> 처리 -> Response
        // 이부분은 전강의와 같은 내용
        Reader reader = new InputStreamReader(socket.getInputStream());

        CharBuffer charBuffer = CharBuffer.allocate(1_000_000);
        reader.read(charBuffer);

        charBuffer.flip();
        System.out.println(charBuffer.toString());

        // 3.5 Response
        String body = """
                <!DOCTYPE html>
                <html lang="ko">
                    <head>
                        <title>예제></title>
                    </head>
                    <body>
                        Hello, World!
                    </body>
                </html>
                """;
        byte[] bytes = body.getBytes();
        String message = "" +
                "HTTP/1.1 200 OK\n" +
                "Content-Type: text/html; charset=UTF-8\n" +
                "Content-Length: " + bytes.length + "\n" +
                "\n" +
                body;
        // Conetent-Type, Content-Lentgh 를 더해주는게 좋다
        // 마지막에 한줄 더 넣지않으면 안되는 경우가 있기 때문에 \n 추가하였음 (아직 에러는 발견하지 못함)
        
        // >> 이부분 과제할때 \n  안넣어줫다가 응답이 원하는대로 안나와서 추가해준 경험 생김..


        Writer writer = new OutputStreamWriter(socket.getOutputStream());
        writer.write(message);
        writer.flush();

        // 4. Close
        socket.close();
    }

}
```



* 추가로 과제하다 \n때문에 곤욕..? 을 치뤄서 추가하였었음&#x20;
