# [Unity] Way To The Rose - 뱀서라이크 게임 개발 (2025.10 ~)

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

### 🔹 에너미

- **스테이트 패턴 기반 에너미 행동 AI 구현**

<img src="https://github.com/user-attachments/assets/96f6bd40-a198-4b83-aaa2-675834556436" width="80%">

에너미가 가지는 스테이트의 기반 구조를, ScriptableObject를 상속하는 추상 클래스 EnemyState로 정의 <br>

<img src="https://github.com/user-attachments/assets/24dec04e-9a71-4a7f-b3ab-2af787502960" width="50%">

각 에너미 별로 사용할 스테이트를, EnemyState 클래스를 상속한 개별 클래스로 정의 <br>

<img src="https://github.com/user-attachments/assets/919f9f48-0de8-473c-97a8-bef0df0ccafc" width="50%">

각 스테이트 클래스의 SO를 에너미의 데이터에 등록하여, 에너미가 사용할 스테이트를 직관적으로 설정 <br>

<img src="https://github.com/user-attachments/assets/3541eb77-6468-4f73-9d5d-96b59d48cea3" width="50%">

게임 내 상황에 따라 에너미의 스테이트를 전환 (기존 스테이트의 탈출 -> 새로운 스테이트로 진입) <br>  <br>

- **데이터 기반 설계 : 에너미 테이블의 데이터를 ScriptableObject로 자동 변환 -> 실시간 반영**

<img src="https://github.com/user-attachments/assets/d27a0ef1-c8e5-4c24-8ff6-19f68abe4fcf" width="60%">

에너미의 수치적 데이터를 구글 스프레드시트에서 테이블(CSV)로 관리 <br>

<img src="https://github.com/user-attachments/assets/03e49f06-fe12-4efd-a5c3-ec13c0abf3c3" width="60%">

커스터마이즈된 에디터의 기능을 통해 스프레드시트에서 테이블(CSV)을 다운로드 <br>

<img src="https://github.com/user-attachments/assets/21813579-8020-4a6c-957c-9203dd8fed26" width="65%">
<img src="https://github.com/user-attachments/assets/9265a625-53fe-4f67-962f-e65ebc7430e3" width="30%">

다운로드받은 테이블을 CsvHelper를 통해 파싱하여 EnemyData SO를 생성 <br>

<img src="https://github.com/user-attachments/assets/c65f5718-d80c-4777-9c4b-084702bca68a" width="30%">
<img src="https://github.com/user-attachments/assets/82713ff7-5a45-43fc-98fb-68b5abedfcc5" width="40%"> <br>

<img src="https://github.com/user-attachments/assets/0563dd5e-d84b-4a8a-8f91-9148c25d482b" width="40%">

테이블 데이터에 따라 자동으로 생성된 EnemyData SO -> 에너미 생성시 해당 데이터들을 이용하여 수치 초기화


### 🔹 스테이지 시스템 (청크 단위 구성, 청크 랜덤 생성, 구조물 랜덤 배치, 청크/구조물 프리팹 데이터화)

### 🔹 오브젝트 (제단 등)

