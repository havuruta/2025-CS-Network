# 04-3 TCP의 오류·흐름·혼잡 제어

## 📌 학습 목표
- 해당 챕터의 개념 정리

## ❓ 확인 문제

### Q1. TCP의 오류 제어, 흐름 제어, 혼잡 제어에 대한 설명 중 틀린 것은?

1️. 오류 제어는 데이터가 손실되거나 손상된 경우 재전송하는 메커니즘을 포함한다.

2️. 흐름 제어는 송신자가 수신자의 처리 속도에 맞춰 데이터 전송 속도를 조절하는 기능이다.

3️. 혼잡 제어는 송신자의 네트워크 상태를 고려하지 않고 항상 최대 속도로 데이터를 전송하도록 한다.

4. 혼잡 제어는 네트워크의 혼잡 상태를 감지하고 전송 속도를 조절하는 기능을 수행한다.

<details>
<summary>정답</summary>

- **3. 혼잡 제어는 송신자의 네트워크 상태를 고려하지 않고 항상 최대 속도로 데이터를 전송하도록 한다. X**   
  - TCP의 혼잡 제어는 네트워크의 혼잡 상태를 감지하고, 혼잡이 발생하면 전송 속도를 낮추는 방식으로 작동한다.

**[해설]**

- **1️. 오류 제어는 데이터가 손실되거나 손상된 경우 재전송하는 메커니즘을 포함한다. O**   
  -  TCP는 오류 제어 기능을 통해 데이터가 손실되거나 손상될 경우 재전송하는 기능을 제공합니다.


- **2. 흐름 제어는 송신자가 수신자의 처리 속도에 맞춰 데이터 전송 속도를 조절하는 기능이다. O**   
  - 흐름 제어는 송신자의 전송 속도를 조절하여 수신자가 처리할 수 있도록 도와줍니다.
  

- **4. 혼잡 제어는 네트워크의 혼잡 상태를 감지하고 전송 속도를 조절하는 기능을 수행한다. O** 
  - 혼잡 제어는 네트워크 상태를 고려하여 과부하를 방지하는 기능을 합니다.
  
---

</details> 

### Q2. TCP 재전송 기법에 대한 설명으로 틀린 것을 고르시오.

1. 대표적인 세 가지 방법으로 Stop-And-Wait, Go-Back-N, Selective Repeat이 있다.
2. Stop-And-Wait은 확인 응답을 받기 전까지, 새로운 메세지를 보내지 않는 방식이다.
3. Go-Back-N은 확인 응답을 받지 않더라도, 새로운 메세지를 보내는데, 도중에 잘못 전송된 세그먼트가 발생하면 해당 세그먼트만 다시 보내준다.
4. 오늘날 대부분의 호스트는 Selective Repeat ARQ를 지원한다.

<details>
<summary>정답</summary>

##### 3. Go-Back-N은 확인 응답을 받지 않더라도, 새로운 메세지를 보내는데, 도중에 잘못 전송된 세그먼트가 발생하면 해당 세그먼트만 다시 보내준다. -> X

**[해설]**
도중 잘못 전송된 세그먼트가 발생하면 해당 세그먼트만 다시 보내는 방법은 Selective Repeat ARQ이다.

Go-Back-N의 경우, 확인 응답을 받은 후, 손실된 세그먼트임이 판단되면, 해당 세그먼트 부터 다시 보낸다.

</details>

### Q3. 다음 중 TCP 흐름 제어에서 사용되는 슬라이딩 윈도우에 대한 설명으로 옳지 않은 것은?

#### 1. 슬라이딩 윈도우에서 윈도우는 송신 호스트가 파이프라이닝할 수 있는 최소량에 해당된다.

#### 2. 송신 호스트만 전송 시 윈도우를 고려하는 것이 아닌 수신 호스트 또한 윈도우를 고려한다.

#### 3. TCP 세그먼트 내에는 윈도우 필드가 존재하며, 수신 윈도우의 크기가 명시된다.

#### 4. 송수신 호스트에서 세그먼트 송수신 여부에 따라 윈도우를 움직여 TCP 흐름을 제어하는 기법이다.

<details>
<summary>정답</summary>

#### 1. 슬라이딩 윈도우에서 윈도우는 송신 호스트가 파이프라이닝할 수 있는 최소량에 해당된다.
- 윈도우는 송신 호스트가 확인 응답 없이 한번에 전송 가능한 최대량을 의미합니다.
- 송신 호스트는 수신 호스트가 알려주는 수신 측 윈도우를 토대로 세그먼트를 전송합니다.

---

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
