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

[![Watch the video](https://img.youtube.com/vi/F6DzPczeOM4/hqdefault.jpg)](https://www.youtube.com/watch?v=F6DzPczeOM4&t=4s)

1. 유저,글 CRUD 설계 및 기능 구현
2. Spring Security를 활용한 로그인 인증 및 기능구현
3. Kakao login api를 활용한 로그인,로그아웃 기능구현
4. Naver mail api를 활용한 비밀번호 찾기 및 변경 기능구현
5. 글 공개범위 필터링 구현

<hr/>

### 데이터 베이스 설계

![Yoonlee3 DB](https://github.com/user-attachments/assets/1e2e1bd1-4ec0-488a-9698-80bafa37e77a)

<hr/>

### 트러블 슈팅
<details>
  <summary><strong>1. 카카오 로그아웃 실패</strong></summary>
  • <strong>문제 상황</strong>: 카카오 로그아웃 시, 세션 쿠키가 정상적으로 삭제되지 않아 사용자가 로그아웃해도 자동으로 로그인 상태가 유지되는 현상이 발생 <br/> → 보안 취약점 존재
  <br/>
  • <strong>원인 분석</strong>: 카카오 로그아웃 API 호출 또는 로그아웃 URL 리다이렉션이 누락<br/> → 카카오 측 세션 및 인증 토큰이 미해제
  <br/>
  • <strong>해결 방법</strong>: Spring Security 설정에 카카오 로그아웃 URL을 명시하여 로그아웃 요청 시 해당URL로 리다이렉트되도록 구현<br/> → 카카오 세션을 종료시키고, 클라이언트 쿠키도 정상적으로 삭제되도록 처리

</details>
<details>
  <summary><strong>2. 유저 연결테이블에 따른 탈퇴실패</strong></summary>
  • <strong>문제 상황</strong>: 사용자가 그룹에 가입, 게시글 등 연관된 데이터를 보유한 상태에서 탈퇴 시도  <br/> → 데이터베이스 제약조건으로 인해 사용자 삭제가 실패
  <br/>
  • <strong>원인 분석</strong>: 사용자 엔티티와 연관된 다른 엔티티(예: 그룹, 게시글 등) 간의 외래키 관계 존재<br/> → 연관 데이터가 삭제 또는 해제되지 않아 제약 조건을 위반
  <br/>
  • <strong>해결 방법</strong>: JPA 엔티티에 cascade = CascadeType.REMOVE 설정을 적용<br/> → 사용자가 삭제 시 연관된 엔티티도 함께 삭제 처리<br/> → 무결성 문제를 해결하고, 사용자 탈퇴가 원활히 진행되도록 개선

</details>
<details>
  <summary><strong>3. 그룹장인 유저 탈퇴실패</strong></summary>
  • <strong>문제 상황</strong>: 그룹장 권한을 보유한 사용자가 탈퇴를 시도할 경우, 해당 그룹의 연결 관계로 인해 탈퇴 불가능
  <br/>
  • <strong>원인 분석</strong>: 그룹 엔티티가 다수의 사용자와 연관되어 있고, 그룹장의 권한 이전 로직이 없어서 그룹장이 탈퇴 시 그룹도 같이 삭제되는 현상 발생
  <br/>
  • <strong>해결 방법</strong>: 그룹장 탈퇴 시점에 해당 그룹 내 가입일 기준으로 다음 순번의 사용자에게 자동으로 그룹장 권한을 양도하는 권한 이전 로직을 구현 만약 그룹에 그룹장 외에 다른 회원이 없을 경우, 그룹 자체도 함께 삭제되도록 처리

</details>
<details>
  <summary><strong>4. Git 병합오류</strong></summary>
  • <strong>문제 상황</strong>: 엔티티, 서비스, 컨트롤러 파일에서 다수 개발자가 동시에 작업하며 병합 충돌이 빈번하게 발생
  <br/>
  • <strong>원인 분석</strong>: 세밀하지 않은 파트 분배 및 중복된 파일로 여러 사람이 개발하여 충돌문제가 발생
  <br/>
  • <strong>해결 방법</strong>: 팀원들에게 개발파일을 받아 수동으로 병합후 Git main브랜치에 Push하는 방식으로 해결

</details>
<hr/>

### 느낀 점

![느낀점](https://github.com/user-attachments/assets/d10d43ec-55ad-490e-a0ab-fd0251924a74)
