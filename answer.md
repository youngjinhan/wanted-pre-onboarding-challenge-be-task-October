(1) 
동시성 제어를 활용하여 이를 해결한다.
하나의 트랜잭션이 read를 할 때 공유락(LS, Shared Lock)을 걸고, read/write를 할 때 사용하는 배타락(LX, Exclusive Lock)을 걸어 데이터의 무결성을 보장하도록한다.
Read 작업은 서로 영향을 주지 않으므로 다른 트랜잭션도 Shared-Lock이 설정된 X에 대해서 Shared-Lock을 동시에 설정할 수 있다. 
Write는 데이터에 영향을 주는 작업이므로 다른 트랜잭션은 Exclusive-Lock을 설정한 데이터 항목 X에 대해서 어떠한 lock도 설정할 수 없다.

(2)
TCP : 
- 연결형 서비스로 가상 회선 방식을 제공한다.
- 3-way handshaking과정을 통해 연결을 설정하고 4-way handshaking을 통해 해제한다.
- 흐름 제어 및 혼잡 제어.
- 높은 신뢰성을 보장한다.
- UDP보다 속도가 느리다.
- 서버와 클라이언트는 1대1로 연결된다.
- 스트림 전송으로 전송 데이터의 크기가 무제한이다.
- 패킷에 대한 응답을 해야하기 때문에(시간 지연, CPU 소모) 성능이 낮다.
- Streaming 서비스에 불리하다.(손실된 경우 재전송 요청을 하므로)

UDP:
- 비연결형 서비스로 데이터그램 방식을 제공한다
- 정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않는다.
- UDP헤더의 CheckSum 필드를 통해 최소한의 오류만 검출한다.
- 신뢰성이 낮다
- TCP보다 속도가 빠르다
- 서버와 클라이언트는 1대1, 1대N, N대M 등으로 연결될 수 있다.
- 데이터그램(메세지) 단위로 전송되며 그 크기는 65535바이트로, 크기가 초과하면 잘라서 보낸다.
- 흐름제어(flow control)가 없어서 패킷이 제대로 전송되었는지, 오류가 없는지 확인할 수 없다.
- 파일 전송과 같은 신뢰성이 필요한 서비스보다 성능이 중요시 되는 경우에 사용된다.

(3) 
 - 브라우저를 열어 주소창에 www.naver.com을 입력한다.   
- (www.naver.com)는 도메인 네임으로 되어있기 때문에 DNS에 도메인을 검색하기 위한 요청을 보낸다.
- DNS는 일련의 과정을 거친 후 (www.naver.com)에 대응하는 ip주소를 응답으로 돌려준다.
- 받은 ip주소를 사용하여 TCP통신을 통해 해당 ip서버에 요청을 보낸다.
- 요청을 받은 서버(www.naver.com)는 요청 내용에 대한 일련에 처리 과정을 거처 응답 메시지를 만든다.
- 응답메시지를 TCP통신을 통해 다시 클라이언트에게 전송한다.
- 브라우저는 받은 응답메시지를 HTTP 프로토콜을 사용하여 웹페이지를 구성하며 사용자에게 Naver 화면을 보여준다.




(4) 
Java의 설계적 결함 중 한가지
- Unsigned integer types가 없다.
자바에는 기본적으로 c, c++등에서 존재하는 unsigned 자료형이 존재하지 않는다.
암호학과 같이 매우 큰 양의 정수를 활용해 다양한 처리를 하는 분야에서 사용하기에 부적합할 수 있다.
2의 보수 표현이나 비트관점에서의 표현을 잘 이해하고 사용하려는 노력을 기울인다면 해결할 수 있는 문제이기는 하지만 개발할 때의 추가적인 노력이 필요하다.



(5) 
HashMap의 동작원리
Java8에서 HashMap에서 기본적으로 사용하는 방식은 Separate Channing이다.
그리고 데이터의 개수가 많아지면 Separate Chaining에서 링크드 리스트 대신 트리를 사용한다.
링크드 리스트를 사용할 것인가 트리를 사용할 것인가에 대한 기준은 하나의 해시 버킷에 할당된 키-값 쌍의 개수이다. Java 8 HashMap에서는 상수 형태로 기준을 정하고 있다. 하나의 해시 버킷에 8개의 키-값 쌍이 모이면 링크드 리스트를 트리로 변경한다. 만약 해당 버킷에 있는 데이터를 삭제하여 개수가 6개에 이르면 다시 링크드 리스트로 변경한다. 트리는 링크드 리스트보다 메모리 사용량이 많고, 데이터의 개수가 적을 때 트리와 링크드 리스트의 Worst Case 수행 시간 차이 비교는 의미가 없기 때문이다. 8과 6으로 2 이상의 차이를 둔 것은, 만약 차이가 1이라면 어떤 한 키-값 쌍이 반복되어 삽입/삭제되는 경우 불필요하게 트리와 링크드 리스트를 변경하는 일이 반복되어 성능 저하가 발생할 수 있기 때문이다.

Java 8 HashMap에서는 Entry 클래스 대신 Node 클래스를 사용한다. Node 클래스 자체는 사실상 Java 7의 Entry 클래스와 내용이 같지만, 링크드 리스트 대신 트리를 사용할 수 있도록 하위 클래스인 TreeNode가 있다는 것이 Java 7 HashMap과 다르다.

이때 사용하는 트리는 Red-Black Tree인데, Java Collections Framework의 TreeMap과 구현이 거의 같다. 트리 순회 시 사용하는 대소 판단 기준은 해시 함수 값이다. 해시 값을 대소 판단 기준으로 사용하면 Total Ordering에 문제가 생기는데, Java 8 HashMap에서는 이를 tieBreakOrder() 메서드로 해결한다.

해시 버킷의 개수가 적다면 메모리 사용을 아낄 수 있지만 해시 충돌로 인해 성능상 손실이 발생한다. 그래서 HashMap은 키-값 쌍 데이터 개수가 일정 개수 이상이 되면, 해시 버킷의 개수를 두 배로 늘린다. 이렇게 해시 버킷 개수를 늘리면 해시 충돌로 인한 성능 손실 문제를 어느 정도 해결할 수 있다.

해시 버킷 개수의 기본값은 16이고, 데이터의 개수가 임계점에 이를 때마다 해시 버킷 개수의 크기를 두 배씩 증가시킨다. 버킷의 최대 개수는 230개다. 그런데 이렇게 버킷 개수가 두 배로 증가할 때마다, 모든 키-값 데이터를 읽어 새로운 Separate Chaining을 구성해야 하는 문제가 있다. HashMap 생성자의 인자로 초기 해시 버킷 개수를 지정할 수 있으므로, 해당 HashMap 객체에 저장될 데이터의 개수가 어느 정도인지 예측 가능한 경우에는 이를 생성자의 인자로 지정하면 불필요하게 Separate Chaining을 재구성하지 않게 할 수 있다.

해시 버킷 크기를 두 배로 확장하는 임계점은 현재의 데이터 개수가 'load factor * 현재의 해시 버킷 개수'에 이를 때이다. 이 load factor는 0.75 즉 3/4이다. 이 load factor 또한 HashMap의 생성자에서 지정할 수 있다.

출처 : 
- https://mangkyu.tistory.com/30
- https://mangkyu.tistory.com/15
- https://develaniper-devpage.tistory.com/88
- https://velog.io/@xogml951/%EC%9E%90%EB%B0%94-%EC%84%A4%EA%B3%84-%EA%B2%B0%ED%95%A8
- https://d2.naver.com/helloworld/831311
