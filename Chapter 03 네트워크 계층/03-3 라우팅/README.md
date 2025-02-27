# 03-3 라우팅

## 📌 학습 목표
- 해당 챕터의 개념 정리

## ❓ 확인 문제
### Q1. 다음 중 정적 라우팅과 동적 라우팅에 대한 설명으로 옳지 않은 것은 무엇인가요?

1️. 정적 라우팅은 관리자가 직접 라우팅 테이블을 설정해야 하며, 네트워크 변화에 따라 수동으로 수정해야 한다.

2️. 동적 라우팅은 RIP, OSPF, BGP와 같은 라우팅 프로토콜을 이용하여 자동으로 최적 경로를 선택한다.

3️. 정적 라우팅은 소규모 네트워크에서 관리가 용이하며, 보안성이 높다.

4️. 동적 라우팅은 고정된 경로를 사용하므로 네트워크 상태 변화에 빠르게 대응할 수 없다.

<details>
<summary>정답</summary>

- **4️. 동적 라우팅은 고정된 경로를 사용하므로 네트워크 상태 변화에 빠르게 대응할 수 없다. X**   
  - 	동적 라우팅은 네트워크 상태 변화에 따라 자동으로 최적의 경로를 갱신하므로, 빠르게 대응할 수 있습니다.

**[해설]**

- **1. 정적 라우팅은 관리자가 직접 라우팅 테이블을 설정해야 하며, 네트워크 변화에 따라 수동으로 수정해야 한다. **   
  - 정적 라우팅(Static Routing)은 관리자가 직접 경로를 설정하므로, 네트워크 변경이 있을 경우 수동으로 수정해야 합니다.

- **2. 동적 라우팅은 RIP, OSPF, BGP와 같은 라우팅 프로토콜을 이용하여 자동으로 최적 경로를 선택한다.  **   
  - 동적 라우팅(Dynamic Routing)은 라우팅 프로토콜을 사용하여 자동으로 최적의 경로를 결정하고, 변경 사항을 반영합니다.
  
- **3. 정적 라우팅은 소규모 네트워크에서 관리가 용이하며, 보안성이 높다. **
  - 정적 라우팅은 불필요한 라우팅 정보를 공유하지 않아 보안성이 높고, 소규모 네트워크에서 효율적으로 사용됩니다.
---

</details>

### Q2. 다음 설명을 읽고 라우팅 테이블에 명시되는 정보 중 무엇인지 쓰시오

##### 최종 수신지까지 가기 위해 다음으로 거쳐야 할 호스트의 IP주소나, 인터페이스를 의미한다. 게이트웨이라고 명시되기도 한다.

<details>
<summary>정답</summary>

- **다음 홉(next hop)**
---

</details>

### Q3. 다음 중 라우팅 테이블에 명시되는 정보에 대한 설명으로 옳지 않은 것은?

1. 다음 홉(next hop)은 최종 수신지까지 가기 위해 다음으로 거쳐야 할 호스트의 IP 주소나 인터페이스를 말한다.
2. 네트워크 인터페이스는 패킷을 내보낼 통로이다.
3. 라우터가 라우팅 테이블에 있는 경로 중 패킷을 내보낼 경로를 선택할 때는 메트릭이 높은 경로를 선호한다.
4. 라우팅 테이블에 포함되는 정보는 라우팅 방식과 호스트 환경에 따라 달라질 수 있다. 

<details>
<summary>정답</summary>

③ 라우터가 라우팅 테이블에 있는 경로 중 패킷을 내보낼 경로를 선택할 때는 메트릭이 높은 경로를 선호한다.

**[해설]**  
라우팅 테이블(Routing Table)은 라우터 또는 호스트가 네트워크 패킷을 올바른 목적지로 전달하기 위해 참조하는 정보 테이블이다.
라우팅 테이블에는 네트워크 주소, 넥스트 홉(Next Hop), 인터페이스, 메트릭(Metric) 등이 포함된다.
라우터는 이 정보를 활용하여 최적의 경로를 결정하고 패킷을 전송한다.

1️⃣ 다음 홉(Next Hop)은 최종 수신지까지 가기 위해 다음으로 거쳐야 할 호스트의 IP 주소나 인터페이스를 말한다. ✅ (O)
- 라우팅 경로는 목적지까지 바로 연결되는 것이 아니라, 여러 개의 중간 장치를 거쳐 이동한다.
- **다음 홉(Next Hop)**은 현재 위치에서 다음으로 패킷을 전달해야 할 라우터나 인터페이스의 주소를 의미한다.
- 목적지까지 가기 위해 필수적인 정보이므로 라우팅 테이블에 포함된다.

2️⃣ 네트워크 인터페이스는 패킷을 내보낼 통로이다. ✅ (O)
- **네트워크 인터페이스(Network Interface)**는 패킷을 전송할 **물리적인 출구(인터페이스)**를 의미한다.
- 예를 들어, 이더넷 포트(eth0), Wi-Fi(wlan0), 특정 네트워크 어댑터 등이 네트워크 인터페이스가 될 수 있다.
- 패킷이 어느 인터페이스를 통해 전송될지를 결정하는 것도 라우팅 테이블의 중요한 역할이다.

3️⃣ 라우터가 라우팅 테이블에 있는 경로 중 패킷을 내보낼 경로를 선택할 때는 메트릭이 높은 경로를 선호한다. ❌ (X) → 메트릭이 낮을수록 우선순위가 높다.
- **메트릭(Metric)**은 특정 경로의 비용(cost) 또는 우선순위(priority)를 나타내는 값이다.
- 라우팅 프로토콜(RIP, OSPF, BGP 등)은 메트릭 값을 이용하여 최적의 경로를 선택한다.
- 일반적으로 메트릭 값이 낮을수록 더 효율적인 경로이므로, 라우터는 메트릭이 낮은 경로를 우선적으로 선택한다.

4️⃣ 라우팅 테이블에 포함되는 정보는 라우팅 방식과 호스트 환경에 따라 달라질 수 있다. ✅ (O)
- 라우팅 테이블은 고정된 구조가 아니라, 라우팅 방식과 환경에 따라 다르게 구성될 수 있다.
- **정적 라우팅(Static Routing)**을 사용할 경우 관리자가 직접 경로를 지정하며,
- **동적 라우팅(Dynamic Routing)**을 사용할 경우 RIP, OSPF, BGP 등의 라우팅 프로토콜을 통해 자동으로 경로가 설정된다.
- 네트워크 환경에 따라 경로 업데이트 빈도, 라우팅 알고리즘, 포함되는 정보 등이 달라질 수 있다.

---

</details>

### Q4. 다음 중 라우팅 프로토콜에 대한 설명으로 올바른 것은?

#### 1️⃣  RIP는 링크 상태 정보를 기반으로 경로를 설정한다.

#### 2️⃣ OSPF는 거리 벡터 알고리즘을 사용하여 경로를 설정한다.

#### 3️⃣ BGP는 AS(Autonomous System) 간의 경로를 설정하는 프로토콜이다.

#### 4️⃣ 정적 라우팅은 네트워크 변화에 따라 자동으로 경로를 갱신한다.

<details>
<summary>정답</summary>

**3️⃣ BGP는 AS(Autonomous System) 간의 경로를 설정하는 프로토콜이다.**  

**[해설]**

#### 1️⃣ RIP는 ***거리 벡터 알고리즘***을 사용하여 경로를 설정한다.

#### 2️⃣ OSPF는 ***링크 상태 알고리즘***을 사용하며, 네트워크의 전체 토폴로지를 유지하며 경로를 계산한다.

#### 4️⃣ 정적 라우팅은 관리자가 직접 경로를 설정해야 하며, 네트워크 변화가 발생해도 자동으로 경로가 변경되지 않는다.

#### ※ BGP(Border Gateway Protocol)는 AS간의 라우팅을 담당하는 유일한 EGP(Exterior Gateway Protocol)로, 실제로는 AS 간의 통신을 가능하게 하는 프로토콜이다.

</details>

### Q5. 다음 중 아래 설명에 해당하는 라우팅 프로토콜은 무엇인가?
- 대표적인 IGP 라우팅 프로토콜로, 링크 상태를 사용하는 라우팅 프로토콜이다.
- 라우터들의 연결 관계, 연결 비용 등 현재 네트워크의 상태 등이 포함된 링크 상태 데이터베이스를 기반으로 최적 경로를 선택한다.

#### 1️⃣ EGP

#### 2️⃣ BGP

#### 3️⃣ AS-PATH

#### 4️⃣ OSPF

<details>
<summary>정답</summary>

#### 4️⃣ OSPF
- OSPF는 링크 상태 라우팅 프로토콜로, 링크 상태 데이터베이스를 기반으로 현재 네트워크 구성을 그려 최적 경로를 선택합니다.
- 링크 상태 데이터베이스에는 라우터들의 연결 관계, 연결 비용 등의 데이터를 활용한 현재 네트워크의 상태가 그래프의 형태로 저장됩니다.

---

</details>


### **Q6. BGP(Border Gateway Protocol) 프로토콜은 무엇인가요?**  

<details>  
<summary> 정답 </summary>  

#### **BGP(Border Gateway Protocol)란?**  

- BGP는 인터넷 상에서 자율 시스템(AS, Autonomous System) 간의 최적 경로를 결정하는 **동적 라우팅 프로토콜** 
- ISP 및 대규모 네트워크에서 사용되며, **라우팅 정보를 교환** 하고 **인터넷 트래픽을 관리**하는 핵심 프로토콜
- BGP는 최적의 경로를 자동으로 선택할 뿐만 아니라, 비용, 정책, 보안 설정 등을 고려한 **정책 기반 라우팅** 을 수행
- 네트워크 장애 발생 시 대체 경로를 선택하여 인터넷 연결을 유지할 수 있습니다.

---

#### **BGP 설정 오류 사례**
- **2021년 10월 25일 KT 네트워크 장애 사건**
- **BGP 설정 오류**로 인해 잘못된 경로 정보가 인터넷에 전파되면서 **KT의 전국적인 인터넷 장애**가 발생함.  
- 일반적으로 BGP는 네트워크 경로를 동적으로 설정하지만, **잘못된 설정이 전파되면 대규모 서비스 장애로 이어질 위험이 있음**.  
- KT 사건에서는 **잘못된 BGP 경로가 ISP 네트워크 전반으로 확산**되면서 **인터넷 서비스 중단**을 초래함.  

#### **BGP 설정 오류를 방지하기 위한 보완 방안**  
- **BGP RPKI(Resource Public Key Infrastructure) 적용**  
  - BGP 경로를 검증하여 신뢰할 수 있는 경로만 사용하도록 보안성을 강화할 수 있음.  
- **BGP 설정 변경 시 사전 검증**  
  - 시뮬레이션 환경에서 BGP 설정을 검증한 후 적용하여 **잘못된 경로가 전파되는 것을 방지**.  
- **라우팅 필터링 및 정책 강화**  
  - 허용된 네트워크 경로만 전파되도록 **BGP 필터링 정책을 적용**하여 오류를 최소화함.  
- **자동화된 네트워크 모니터링 도입**  
  - BGP 라우팅 경로를 실시간 감시하고 **비정상적인 경로 변경이 감지되면 자동으로 차단하는 시스템을 구축**.  

---

- BGP는 전 세계 인터넷을 연결하는 핵심 프로토콜로, **네트워크 장애 시** 자동으로 최적의 경로를 선택하여 **인터넷 연결을 유지**할 수 있는 강력한 기능을 제공합니다. 하지만, 설정 오류가 발생하면 광범위한 네트워크 장애로 이어질 수 있으므로 **보안 강화 및 모니터링 시스템**이 필수적입니다.

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
