# HTTP CLIENT

Tcp/ip 통신

슬래쉬가 있을 경우 프로토콜을 얘기하는건 아님.

\


제일 많이 쓰이기때문에 tcp ip 를 부름

\


Tcp > 연결이 필요ㅡ 전달 및 순서가 보장 (전화기)

\


UDP > 연결하지 않고 데이터를 보냄. 전달 및 순서를 보장하지 않음. (편지)

\*\*해당 비유를 잘 기억해두면 기억하기 쉬울것 같음\


tcp나 udp를 어떻게 쓸것인가에 대해\


Socket 이란 키워드를 기억하자\


Socket 과 socket api 가 별개라고 생각하고 기억하자\


Socket api를 이용해서 socket 을 사용하자 . (공구통에서 공구를 쓴다고 생각하자)



Java 에서는 키보드 입력, 화면 출력, 파일 입출력  >> 이런게 stream으로 다룰수 있다.

java8의 stream 과 헷갈리지말것 (input stream, outputstream을 생각하자)

\


[Example.com](http://example.com) 을 많이 이용해보자 http, https 둘다 접근 가능

\


옵션 엔터 버튼으로 인텔리제이에서 맥북기준 많은걸 할수잇다(임포트, 객체완성등등..)

이부분은 따로 중간중간 나오는 단축키들을 꿀팁처럼 작성해 놔야할것같다. (아직 맥린이니까..)



http client 실습 코드

```
     private void run() throws IOException {
        // 연결 전
        System.out.println("Hello world!");

        //Socket은 Closeable 을 상속 받기 때문에 close를 따로안하고 try resource 사용 가능
        try (Socket socket = new Socket("example.com", 80)) {
            // 연결 완료 후
            System.out.println("connect! ");

            //request
            
            //java 17 버전에서 나온 기능을 사용해봤음
            String message = """
                    GET / HTTP/1.1
                    Host:example.com
                                    
                    """;

            Writer writer = new OutputStreamWriter(socket.getOutputStream());

            writer.write(message);
            //writer 사용 시 flush를 사용해야한다.
            writer.flush();
            //유니코드로 처리하기 위해서 getBytes를 사용
            socket.getOutputStream().write(message.getBytes());

            System.out.println("Request!!");
            // 여기까지 request를 위한 준비


            InputStream inputStream = socket.getInputStream();
            Reader reader = new InputStreamReader(socket.getInputStream());
            CharBuffer charBuffer = CharBuffer.allocate(1_000_000);

            reader.read(charBuffer);

            //flip 을 해줘야 스트링으로 변환이 잘 됨.
            charBuffer.flip();

            String text = charBuffer.toString();

            //reader 사용안하는 방법.
//        byte[] bytes = new byte[1_000_000];
//        int size = inputStream.read(bytes);
//
//        //읽어온 데이터
//        byte[] data = Arrays.copyOf(bytes, size);
//        String text = new String(data);

            System.out.println(text);
        }
        //       socket.close();
        System.out.println("Complete");

    }
```



코딩 강의를 보면서 드는 생각은 내가 어떤 클래스를 쓸때 적혀있는 문서들을 확인해보는 습관들 들여야 할것 같다.

