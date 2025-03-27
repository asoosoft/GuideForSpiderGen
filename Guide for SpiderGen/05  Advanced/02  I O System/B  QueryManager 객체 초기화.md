# B. QueryManager 객체 초기화

**1. I/O 데이터 통신을 위해서는 QueryManager 객체를 생성하고 초기화 해야 합니다.**

**2. 대부분 초기화는 각 프로젝트 Application 파일 (프로젝트명App.js)의 onReady 메소드에 추가합니다.**

```javascript
 
onReady() 
{ 
    super.onReady(); 
 
    // QueryManager 객체 초기화 
    this.queryManager = new QueryManager('info'); 
    let netIo = new WebsocketIO(this.queryManager);  
    this.queryManager.setNetworkIo(netIo); 
    this.queryManager.setQueryBuffer(1024*128, 1024*128, 'euc-kr', 0x20, 0x30); 
    this.queryManager.startManager(‘127.0.0.1’, 80); 
 
    this.setMainContainer(new  APage('main'))
	this.mainContainer.open('Source/MainView.lay')
};  
 
```

**초기화 순서**

1. **QueryManager 객체를 생성합니다.**
2. **QueryManager에서 사용할 IO 객체를 생성합니다.**
3. **HttpIO : http 통신을 위한 I/O 객체 입니다.**
   * WebsocketIO : WebSocket 통신을 위한 I/O 객체 입니다.
   * SocketIO : TCP/IP 소켓 통신을 위한 I/O 객체 입니다.
   * QueryManager에 I/O 객체를 설정합니다.
4. **QueryBuffer 설정**
5. **sendSize : 전송 버퍼 사이즈**
   * recvSize : 수신 버퍼 사이즈
   * charSet : 문자열 인코딩 방식
   * emptyChar : 문자 빈공간 채울 아스키 코드값
   * emptyNumChar : 숫자 빈공간 채울 아스키 코드값
6. **전송을 시작합니다.**
