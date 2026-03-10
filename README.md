# [Unity] Way To The Rose - 뱀서라이크 게임 개발 (2025.10 ~)

![ㅈㅅㅈㅅ](https://github.com/user-attachments/assets/7baad8ee-d22f-482f-a3a8-5c16152e789f)

**🔹 진행 기간 :** 2025.10 ~ 진행중

**🔹 팀 구성 :** 프로그래머 2인, 기획 1인, 사운드 1인, 아트 2인

## 🔷 사용 기술 스택

| 분류 | 내용 |
|------|------|
| **Engine** | Unity 6 |
| **Version Control** | Git |
| **Build Target** | Windows (.exe) |
| **협업 툴** | Notion, Discord |

## 🔷 담당 파트

## 🔹 스테이지 구조

### 🔹 **청크 단위 스테이지 구성**

<img src="https://github.com/user-attachments/assets/464546f2-179c-4b5c-8bea-578e3139cd5c" width="35%">
<img src="https://github.com/user-attachments/assets/2fc9ff04-5fe8-43b0-a8a0-548a7edb03dc" width="35%">

- 지정된 스테이지 구조에 따라 50*50 크기의 **청크들을 종류(일반/제단/보스 청크)별로 랜덤 배치하여 스테이지 구성** <br>

### 🔹 **프리팹 기반 청크 구성**

<img src="https://github.com/user-attachments/assets/e64c3e31-f39a-4aea-9986-2c3d31977fd9" width="60%">
<img src="https://github.com/user-attachments/assets/fe3bc01c-c390-4a22-97d2-931ec1c024f4" width="30%">

- **각 청크**를 **하나의 프리팹**으로 구성
- **타일 기능별 타일맵 분리** / Dictionary로 Enum 값과 대응하여 코드에서 쉽게 접근 <br>

### 🔹 **청크 프리팹의 데이터화**

<img src="https://github.com/user-attachments/assets/57fe7873-0e4d-4269-9554-8d3779830179" width="35%">
<img src="https://github.com/user-attachments/assets/fbebc216-c37d-4155-a9a4-27943a67dffb" width="40%">

- 커스터마이즈한 에디터의 기능을 통해, 청크 프리팹 내 **타일/오브젝트 배치 등의 정보를 담은 ChunkData SO를 생성** <br>

<img src="https://github.com/user-attachments/assets/4b2c0d7a-f31b-4238-a292-8c92ae2f94e2" width="45%">
<img src="https://github.com/user-attachments/assets/b8688163-75fb-4248-9bfb-1ca7caf62413" width="50%">

- 스테이지 생성 중 청크를 배치할 때, **ChunkData SO에 담긴 정보에 따라 실제 씬의 타일맵에 타일 배치 / 오브젝트 배치**
- 이러한 방식을 통해 청크 프리팹들을 직접 씬에 배치하지 않을 수 있으니, **한 씬 내에 타일맵이 과하게 많아지는 문제를 방지** <br>

### 🔹 **청크 내 구조물/오브젝트 랜덤 배치**

<img src="https://github.com/user-attachments/assets/e11a00b7-27a6-4d0c-9523-2037fd023661" width="35%">
<img src="https://github.com/user-attachments/assets/f5de2074-c684-438e-8f75-d64bf7d5252a" width="55%">

- 청크 자체의 타일 및 오브젝트 배치 후 **남은 가용 공간에 구조물/오브젝트를 랜덤 배치**
- **구조물 또한** 청크와 동일하게 **프리팹을 기반으로 구성하고, 데이터화**하여 관리
- **가용 공간의 n%까지만** 추가로 배치할 수 있게 하여, **과한 동선 방해 방지**
- 청크 프리팹에서, **랜덤 배치 제외 영역(NoSpawn)을 지정**할 수 있게 하여 **오류 상황 방지** <br> <br> <br>

## 🔹 에너미

### 🔹 **스테이트 패턴 기반 에너미 AI 구현**

<img src="https://github.com/user-attachments/assets/96f6bd40-a198-4b83-aaa2-675834556436" width="80%">

- 에너미가 가지는 **스테이트의 기반 구조**를, ScriptableObject를 상속하는 추상 클래스 EnemyState로 정의
- **스테이트 진입/유지/탈출** 시점에 동작할 함수를 선언 <br>

<img src="https://github.com/user-attachments/assets/24dec04e-9a71-4a7f-b3ab-2af787502960" width="50%">

- **각 에너미 별로 사용할 스테이트**를, EnemyState 클래스를 상속한 **개별 클래스로 정의**
- 각 스테이트에서 **어떤 행동을 할지** / **어떤 조건이 충족되면 다른 스테이트로 전환할지 정의**<br>

<img src="https://github.com/user-attachments/assets/919f9f48-0de8-473c-97a8-bef0df0ccafc" width="50%">

- 각 스테이트 클래스의 SO를 에너미의 데이터에 등록하여, **에너미가 사용할 스테이트를 직관적으로 설정** <br>

<img src="https://github.com/user-attachments/assets/3541eb77-6468-4f73-9d5d-96b59d48cea3" width="50%">

- 게임 내 상황에 따라 **에너미의 스테이트를 전환** (기존 스테이트의 탈출 -> 새로운 스테이트로 진입) <br>  <br>

### 🔹 **데이터 기반 설계 : 에너미 테이블의 데이터를 ScriptableObject로 자동 변환 -> 실시간 반영**

<img src="https://github.com/user-attachments/assets/d27a0ef1-c8e5-4c24-8ff6-19f68abe4fcf" width="60%">

- **에너미의 수치적 데이터를** 구글 스프레드시트에서 **테이블(CSV)로 관리**
- 기획자가 게임 내 코드/로직에 직접 접근하지 않고 수치 수정 가능<br>

<img src="https://github.com/user-attachments/assets/03e49f06-fe12-4efd-a5c3-ec13c0abf3c3" width="60%">

- 커스터마이즈한 에디터의 기능을 통해 **스프레드시트에서 테이블(CSV)을 다운로드** <br>

<img src="https://github.com/user-attachments/assets/21813579-8020-4a6c-957c-9203dd8fed26" width="65%">
<img src="https://github.com/user-attachments/assets/9265a625-53fe-4f67-962f-e65ebc7430e3" width="30%">

- **다운로드받은 테이블을 CsvHelper를 통해 파싱**하여 **EnemyData SO를 생성** <br>

<img src="https://github.com/user-attachments/assets/c65f5718-d80c-4777-9c4b-084702bca68a" width="30%">
<img src="https://github.com/user-attachments/assets/82713ff7-5a45-43fc-98fb-68b5abedfcc5" width="40%"> <br>

<img src="https://github.com/user-attachments/assets/0563dd5e-d84b-4a8a-8f91-9148c25d482b" width="40%">

- 테이블 데이터에 따라 자동으로 생성된 EnemyData SO -> 에너미 생성시 **해당 데이터들을 이용하여 수치 초기화** <br> <br> <br>




## 🔹 오브젝트 (제단 등)












