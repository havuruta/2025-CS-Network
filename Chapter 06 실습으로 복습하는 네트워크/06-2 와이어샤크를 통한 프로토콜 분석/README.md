# 06-2 와이어샤크를 통한 프로토콜 분석

## 📌 학습 목표
- 해당 챕터의 개념 정리

## ❓ 확인 문제

### Q1. 다음 중 올바르게 줄인 IPv6 주소는 무엇인가?  

**(A)** `2001:db8::ff00::42:8329`  
**(B)** `2001:0db8:0:0:0:ff00:42:8329`  
**(C)** `2001:db8::ff00:42:8329`  

<details>
<summary>정답</summary>

#### **🔹 정답:** **(C)** 
### **🔹 해설:**  
- (A) `::`는 IPv6 주소에서 **한 번만 사용할 수 있음**, 두 번 사용되었기 때문에 잘못된 표현이다.  
- (B) 앞쪽의 `0`을 생략할 수 있음에도 그대로 남아 있어 최적화되지 않았다.  
- (C) IPv6 표준에 맞게 올바르게 줄인 형식이다.  

---

## **🔹 IPv6 주소를 줄여 쓰는 이유**
IPv6 주소는 128비트 길이로 되어 있어 **매우 길다**.  
따라서, **불필요한 0을 줄이고 가독성을 높이기 위해** 다음과 같은 규칙을 사용한다.

### **✅ IPv6 주소 줄이는 규칙**
#### **1. 앞쪽의 0을 생략 가능**  
- `2001:0db8:0000:0000:0000:ff00:0042:8329`  
- → `2001:db8:0:0:0:ff00:42:8329`  

#### **2. 연속된 0을 `::`로 압축 가능 (단, 한 번만 사용 가능)**  
- `2001:db8:0:0:0:ff00:42:8329`  
- → `2001:db8::ff00:42:8329` ✅  

#### **3. 완전히 0인 주소는 `::`로 표현 가능**  
- `0000:0000:0000:0000:0000:0000:0000:0001`  
- → `::1` ✅ (루프백 주소)  

---

## **🔹 Wireshark에서 IPv6 줄이기 적용 예시**
Wireshark는 패킷을 캡처할 때 자동으로 IPv6 주소를 줄여서 보여준다.  
예를 들어, 원래 IPv6 주소가 다음과 같다면: fe80:0000:0000:0000:1a2b:3c4d:5e6f:7g8h

Wireshark에서는 **자동으로 아래와 같이 줄여서 표시**한다: fe80::1a2b:3c4d:5e6f:7g8h


---

## **🔹 IPv6 주소 줄이기의 장점**
✔ **가독성 향상** – IPv6 주소가 너무 길기 때문에 줄이면 더 읽기 쉬움  
✔ **입력 편의성** – 네트워크 엔지니어, 개발자들이 입력할 때 오류 감소  
✔ **Wireshark 등 분석 도구에서 직관적 표현 가능**  

👉 **IPv6 주소 줄이기는 필수적인 기술이며, Wireshark에서도 이를 자동으로 적용한다!** 🚀  

</details>





### Q2. 다음 중 와이어샤크를 통해 프로토콜 분석을 수행할 때, 알 수 있는 것을 모두 고르시오.

1. TCP 연결 종료 (4-way-handshake)
2. TCP 연결 수립 (3-way-handshake)
3. HTTP 요청, 응답 헤더
4. 암호화된 HTTPS 요청의 본문 내용

<details>

#### 정답 1,2,3

<summary>정답</summary>

**[해설]**

- 책에서 읽은 것 처럼, 1, 2, 3번의 경우 바로 확인이 가능하다. 하지만, HTTPS 트래픽은 암호화 되어있기 때문에, 와이어 샤크에서 본문의 내용은 직접 확인할 수 없다. 


</details>

### Q3. ICMP 프로토콜은 주로 어떤 목적으로 사용되는지 설명하시오.

<details>

#### 정답 : 네트워크 상태 점검(도달 가능성 확인, 경로 추적, 오류 메시지 전달 등)

<summary>정답</summary>

**[해설]**

#### ICMP의 주요 기능
1) 도달 가능성 확인
- ping 명령어는 ICMP의 **Echo Request (Type 8)**와 **Echo Reply (Type 0)**를 사용해 상대가 응답 가능한지 확인함.
```sql
No.   Time     Source        Destination   Protocol   Info
1     0.000    192.168.0.2   8.8.8.8       ICMP       Echo (ping) request
2     0.123    8.8.8.8       192.168.0.2   ICMP       Echo (ping) reply
```
2) 경로 추적
- traceroute 명령은 TTL(Time to Live) 값을 1부터 점점 높여가며 라우터 하나씩 거치면서 ICMP Time Exceeded (Type 11) 메시지를 수신함.
```sql
No.   Time     Source        Destination   Protocol   Info
1     0.000    192.168.0.2   8.8.8.8       ICMP       Echo (ping) request TTL=1
2     0.045    10.1.1.1      192.168.0.2   ICMP       Time-to-live exceeded
3     0.100    192.168.0.2   8.8.8.8       ICMP       Echo (ping) request TTL=2
4     0.145    10.1.2.1      192.168.0.2   ICMP       Time-to-live exceeded

```
3) 오류 메시지 전달
- 목적지에 도달할 수 없는 경우 ICMP Type 3 (Destination Unreachable) 메시지가 수신됨.
```sql
No.   Time     Source        Destination   Protocol   Info
1     0.000    192.168.0.2   10.10.10.10   TCP        [SYN]
2     0.150    10.10.10.1    192.168.0.2   ICMP       Destination unreachable (Port unreachable)

```

</details>

### Q4. TCP와 UDP의 차이를 와이어샤크로 분석할 때 어떤 차이점이 있는지 설명하시오.


<details>

#### 정답
- TCP는 연결 지향형 프로토콜로, 통신을 시작하기 전에 3-way 핸드셰이크(SYN, SYN-ACK, ACK)를 통해 연결을 설정함. 이 과정이 와이어샤크에서 순차적으로 보이며, 또한 TCP는 순서 번호, 확인 응답 번호, 재전송 등의 정보가 포함된 패킷이 다수 존재하며, 세션 흐름이 명확히 나타남.

- 반면, UDP는 연결 설정 없이 데이터를 전송하며, 패킷 간 관계가 없어 단순히 요청/응답 패킷만 보임. 와이어샤크에서도 단순한 구조로 나타나고, 세션 추적이 어려움.

<summary>정답</summary>

**[해설]**

#### 와이어샤크 패킷(TCP)
```sql
No.   Source        Destination   Protocol   Info
1     192.168.0.2   93.184.216.34 TCP        SYN
2     93.184.216.34 192.168.0.2   TCP        SYN, ACK
3     192.168.0.2   93.184.216.34 TCP        ACK
4     ...           ...           TCP        [PSH, ACK] HTTP GET

```
- 3-way handshake(SYN → SYN-ACK → ACK)

- 이후에는 시퀀스 번호(seq), 응답 번호(ack), 재전송 표시(retransmission) 등 다양한 정보 확인 가능.

#### 와이어샤크 패킷(UDP)
```sql
No.   Source        Destination   Protocol   Info
1     192.168.0.2   8.8.8.8       UDP        Standard query 0x1234 A ssafy.com
2     8.8.8.8       192.168.0.2   UDP        Standard query response A 93.184.216.34

- 연결 없음, 단순히 요청(Request)과 응답(Response)만 존재

- 시퀀스나 재전송 등의 정보 없음

```
- 3-way handshake(SYN → SYN-ACK → ACK)

- 이후에는 시퀀스 번호(seq), 응답 번호(ack), 재전송 표시(retransmission) 등 다양한 정보 확인 가능.

</details>


### Q5. 제로 데이 패킷 분석

> 제로 데이 공격이 발생한 후 수집된 `quiz02.pcapng` 패킷 덤프 파일이 있다.  
> 네트워크 관리자는 다음과 같은 분석을 요청하였다.  
> - 서버 IP: 141.157.228.12  
> - 클라이언트 IP: 10.1.1.31  

1. 어떤 응용 계층 프로토콜을 이용하여 파일이 전송되었는가?  
2. 파일을 수신한 호스트의 IP 주소는 무엇인가?  
3. 전송된 파일의 이름은 무엇인가?

`TFTP` 필터로 검색하여 나온 데이터들을 요약한 내용이다.

<details>
<summary>패킷 정보 (Frame 6)</summary>

```
Frame 6: 62 bytes on wire (496 bits), 62 bytes captured (496 bits)  
[Protocols in frame: eth:ethertype:ip:udp:tftp]

Ethernet II:  
- Source: NXPSemicondu_00:00:02  
- Destination: Runtop_17:33:2e  
- Type: IPv4 (0x0800)

IP (Internet Protocol):  
- Source IP: 10.1.1.31  
- Destination IP: 141.157.228.12  
- Protocol: UDP  
- Source Port: 1028  
- Destination Port: 69

TFTP (Trivial File Transfer Protocol):  
- Opcode: Read Request  
- Source File: msblast.exe  
- Transfer Type: octet
```

</details>

> `TFTP`는 UDP 기반의 파일 전송 프로토콜로 인증 없이 파일을 전송한다.  
> 이 프로토콜은 악성코드나 제로 데이 공격에 종종 사용되며, 파일을 빠르게 전송할 수 있다.

<details>
<summary>정답</summary>

1. TFTP  
2. 10.1.1.31  
3. msblast.exe

---

### 요약

- **TFTP**는 인증 없이 빠르게 파일을 전송하는 UDP 기반의 프로토콜로, 보안에 취약하다.  
- 이 문제에서는 `msblast.exe`라는 악성 파일이 **클라이언트(10.1.1.31)**로 전송된 상황을 분석하고 있다.
- 패킷 분석 시 다음을 확인할 수 있다:  
  - **Source IP**는 파일을 요청한 클라이언트의 IP 주소  
  - **Source File**은 요청된 파일의 이름

---

### 해설

#### TFTP
- TFTP는 UDP 기반의 단순한 파일 전송 프로토콜로, 인증이나 암호화 없이 파일을 전송하기 때문에 보안상 취약하다.  
- 패킷의 `Protocols in frame` 항목에서 TFTP가 사용되고 있음을 확인할 수 있다.

#### 10.1.1.31
- TFTP에서 파일 전송은 클라이언트가 서버에 요청(Read Request)을 보내고, 서버가 파일을 전송하는 구조다.  
- 이때 요청을 보낸 쪽(IP: 10.1.1.31)이 파일을 받게 되는 클라이언트다.

#### msblast.exe
- TFTP 요청에는 전송할 파일의 이름이 포함되며, `Source File: msblast.exe` 항목에서 이를 확인할 수 있다.  
- 해당 파일은 악성코드이며, 네트워크 전파형 웜으로 알려져 있다.

</details>

### Q6. 위 사례처럼 인증 없이 파일이 전송되는 상황을 고려할 때, 서비스를 개발하거나 운영할 때 발생할 수 있는 보안 사고를 방지하기 위해 개발자가 적용할 수 있는 방법에는 어떤 것이 있나요?

<details>
<summary>정답</summary>

- API 요청에는 반드시 인증을 요구하도록 설계한다.  
  아무나 접근할 수 있는 엔드포인트는 공격에 쉽게 노출될 수 있다.

- 이를 위한 대응 방법 중 하나로 **세션 기반 인증 방식**을 사용할 수 있다.  
  예를 들어, 아래와 같이 세션을 확인하여 인증된 사용자만 데이터를 조회할 수 있도록 제한할 수 있다.

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
    HttpSession session = request.getSession(false); // 기존 세션 가져오기
    
    if (session != null && session.getAttribute("user") != null) {
        response.getWriter().println("비공개 데이터입니다. 사용자: " + session.getAttribute("user"));
    } else {
        response.setStatus(HttpServletResponse.SC_UNAUTHORIZED);
        response.getWriter().println("로그인이 필요합니다.");
    }
}
```

</details>


## 📝 사용법  
### 이렇게 활용해 보세요! ✨  
1. ❓ 확인 문제 아래에 본인이 만든 질문을 추가하세요.  
2. 설명이 길어질 경우, 따로 마크다운 파일을 만들고 링크를 함께 추가해 주세요! 🔗  

### 🔗 링크 추가 방법  
1. 먼저 질문을 작성합니다.  
2. 링크를 적용할 문장을 마우스로 선택합니다.  
3. URL을 붙여넣습니다.  
4. 마크다운 형식으로 `[내용](링크)` 형태로 정리됩니다.  

