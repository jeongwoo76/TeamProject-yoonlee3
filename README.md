# yoonlee3
![스크린샷_27-7-2025_13048_](https://github.com/user-attachments/assets/05e00f73-9ee7-46c6-b830-4c80146b1eb3)

## 배포 사이트
- http://3.39.192.82:8080/

## Team GitHub
- https://github.com/Lee-jaemyeong/team-repository

### 목차
- 1️⃣ [프로젝트 개요](#프로젝트-개요)
- 2️⃣ [기술 스택](#기술-스택)
- 3️⃣ [담당 기능](#담당-기능)
- 4️⃣ [데이터 베이스 설계](#데이터-베이스-설계)
- 5️⃣ [트러블 슈팅](#트러블-슈팅)
- 6️⃣ [느낀 점](#느낀-점)

<hr/>

### 프로젝트 개요
목표 달성을 위한 동기 부여와 소통을 돕기 위해 만든 웹 기반 **일기 공유 플랫폼**입니다.
개인은 자신의 일기를 작성하고 관리할 수 있으며, 선택적으로 다른 사용자와 일기를 공유하거나 그룹을 만들어 함께 목표를 세우고 달성률을 나눌 수 있습니다.

**"기획 배경"** <br/>
기존에 목표 달성을 위한 교환일기 형태의 웹사이트가 매우 제한적이라는 점에 착안하여,
개인적인 동기 부여와 사회적 소통을 동시에 실현할 수 있는 공간을 만들고자 본 프로젝트를 기획하였습니다.
<hr/>

### 기술 스택
⚙️ Back-End
- Spring Boot 2.7.14
- Spring Security 5.0.7
- JPA (Hibernate) 2.7.14
- Lombok 1.18.28
- Spring DevTools 2.7.14

🌐 Front-End
- Thymeleaf 3.0.15
- HTML5 / CSS3 / JavaScript
- jQuery 3.7.1

🗄 Database & Server
- MySQL 8.0.33
- Apache Tomcat 9.0.78

💻 협업 & 배포
- GitHub – 소스코드 버전 관리

<hr/>

### 담당 기능
#### 📺 시연 영상 (이미지 클릭시 유튜브로 이동됩니다.)

[![Watch the video](https://github.com/user-attachments/assets/4230162a-273b-4fd0-9b43-8c85db57b1bd)](https://www.youtube.com/watch?v=fyXjxewcSSE)

1. 유저 팔로우, 언팔로우 맞팔로우 설계 및 기능 구현
2. 유저 차단 설계 및 기능 구현


<hr/>

### 데이터 베이스 설계

![Yoonlee3 DB](https://github.com/user-attachments/assets/1e2e1bd1-4ec0-488a-9698-80bafa37e77a)

<hr/>

### 트러블 슈팅
<details>
  <summary><strong>1. 프론트엔드 팔로우 버튼 undefined 값 문제</strong></summary>
  • <strong>문제 상황</strong>: 서버에서 받아온 일부 사용자 데이터 필드가 null 또는 누락되어, 프론트엔드에서 undefined 값으로 출력되며 UI가 깨짐
  <br/>
  • <strong>원인 분석</strong>: 서버 JSON 데이터에 null/빈 값 포함 → 프론트엔드에서 예외처리 없이 바인딩
  <br/>
  • <strong>해결 방법</strong>: Thymeleaf 내에서 th:if, th:unless 조건문으로 기본값 렌더링 처리하여 UX 안정성 확보
  <br/>
  • <strong>효과</strong>: 서버 응답 스펙 명확화 및 필드 기본값 초기화로 프론트/백엔드 데이터 불일치 최소화
</details>

<details>
  <summary><strong>2. 차단한 사용자가 친구/팔로잉 목록에 계속 노출</strong></summary>
  • <strong>문제 상황</strong>: 차단한 사용자가 여전히 목록에 노출되고, UI에 차단 상태 반영 안 됨
  <br/>
  • <strong>원인 분석</strong>: DB 쿼리에서 차단 상태 조건 누락 → 필터링 미흡
  <br/>
  • <strong>해결 방법</strong>:  
  백엔드 쿼리 수정: 사용자 관계 테이블에서 차단 관계 조건 추가 (예: WHERE blocked = false)
   <br/>
  프론트엔드: 렌더링 시 차단 사용자 추가 필터링 적용
  <br/>
  • <strong>효과</strong>: 차단 기능 신뢰성 강화 및 사용자 경험 향상
</details>

<details>
  <summary><strong>3. 팔로우/차단 후 즉시 UI 반영 안 됨</strong></summary>
  • <strong>문제 상황</strong>: 상태 변경 후에도 UI가 즉시 업데이트되지 않고 새로고침 필요
  <br/>
  • <strong>원인 분석</strong>: API 호출 성공 후에도 프론트엔드 상태 갱신 로직 누락
  <br/>
  • <strong>해결 방법</strong>: 액션 성공 시 isFollowing, isBlocked 상태 직접 업데이트하거나, 데이터 재요청(fetch)으로 UI 동기화
  <br/>
  • <strong>효과</strong>: 변경 사항이 실시간 반영되어 직관적이고 자연스러운 UX 제공
</details>
<hr/>
  
### 느낀 점

![느낀점](https://github.com/user-attachments/assets/c47c49f6-d2d0-4c4c-a34a-ae43752f12ae)
