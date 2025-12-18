# BNK-BOARD-JSON-LAB

순수 **HTML / CSS / JavaScript** 환경에서  
**게시판 UI + JSON 기반 데이터 시딩(seed) + 인증 흐름(MVP)** 을 실험하기 위한 레포지토리이다.

Spring / DB 이전 단계에서  
- 데이터 구조 설계
- 게시판 도메인 분리
- 인증/권한 흐름 최소 구현
- 시드 데이터 관리 방식  
을 검증하는 목적의 실험용 프로젝트다.

---

## 작업기간
2025.12.18 (1일 / 11:00 ~ 16:00, 점심시간 제외)

---

## 화면 미리보기

### index.html (list)  
이미지를 누르면 해당 페이지로 이동합니다.
<a href="https://yingbbang.github.io/bnk-board-html/board/index.html"> 
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/snapshot-index.png"></a>

### view.html (view)
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/snapshot-view.png">

### write.html (write)  
이미지를 누르면 해당 페이지로 이동합니다.
<a href="https://yingbbang.github.io/bnk-board-html/board/write.html"> 
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/snapshot-write.png"></a>

### edit.html (edit)
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/snapshot-edit.png">

### delete.html (delete)
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/snapshot-delete.png">

---

## 설계 문서

### ERD
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/erd.png">

### Data Dictionary
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/data-dictionary.png">

### Code Definition
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/code-definition.png">

---

## 1. 프로젝트 목적

- 프레임워크 없이 게시판 기능 구현
- JSON 기반 게시글 데이터 로딩 및 시딩 실험
- **로그인 / 회원가입 / 권한 가드의 최소 단위 구현**
- 금융권 게시판 도메인 구조 연습
- 추후 Spring + DB 전환을 고려한 구조 검증

※ 본 프로젝트의 로그인/회원가입은 **보안 목적이 아닌 구조·흐름 검증용 데모 구현**이다.

---

## 2. MVP 구현 범위

본 프로젝트는 아래 기능까지만을 **의도적으로 구현**한다.

- 회원가입 (데모, 비밀번호 없음)
- 로그인 / 로그아웃 (localStorage 기반)
- 권한 가드 (USER / ADMIN 최소 분기)
- 게시글 CRUD
- 로그인 상태 기반 접근 차단

관리자 페이지, 실제 인증 서버, 비밀번호 암호화 등은  
**현재 단계에서는 구현 대상에서 제외**한다.

---

## 3. 전체 폴더 구조

```text
BNK-BOARD-JSON-LAB
├─ assets/
│  ├─ css/
│  │  ├─ common.css          # 공통 스타일
│  │  ├─ auth.css            # 로그인/회원가입
│  │  └─ board.css           # 게시판
│  │
│  └─ icons/
│
├─ js/
│  ├─ core/
│  │  ├─ storage.js          # localStorage 기반 가상 DB
│  │  ├─ util.js             # 공통 유틸
│  │  └─ constants.js        # ROLE / STATUS 상수
│  │
│  ├─ auth/
│  │  ├─ auth.js             # 로그인 / 로그아웃
│  │  ├─ signup.js           # 회원가입 (데모)
│  │  ├─ guard.js            # 로그인 / 권한 가드
│  │  └─ user.store.js       # USER 저장소
│  │
│  ├─ board/
│  │  ├─ list.js             # 게시글 목록
│  │  ├─ view.js             # 게시글 상세
│  │  ├─ write.js            # 게시글 작성 (로그인 필요)
│  │  ├─ edit.js             # 게시글 수정
│  │  └─ delete.js           # 게시글 삭제 (상태 변경)
│  │
│  └─ seed/
│     └─ board.seed.js       # 게시판 시드 데이터 로딩
│
├─ auth/
│  ├─ login.html
│  └─ signup.html
│
├─ board/
│  ├─ index.html
│  ├─ view.html
│  ├─ write.html
│  ├─ edit.html
│  └─ delete.html
│
├─ admin/
│  └─ README.md              # 관리자 영역 (구조만 정의)
│
├─ schema/
│  ├─ data-dictionary.html
│  ├─ code-definition.html
│  └─ erd.png
│
└─ README.md
```
---

## 4. 주요 설계 포인트

- 프레임워크 없이 게시판 기능 구현
- JSON 기반 게시글 데이터 로딩 및 시딩 실험
- **로그인 / 회원가입 / 권한 가드의 최소 단위 구현**
- 금융권 게시판 도메인 구조 연습
- 추후 Spring + DB 전환을 고려한 구조 검증
- localStorage를 **가상 DB**로 사용하여 데이터 흐름 통제
- 게시글 작성자(writer)와 행위자(created_by)를 분리한 설계
- 물리 삭제 대신 **상태값 기반 삭제**
- auth / board 도메인 분리로 확장성 확보
- 관리자 기능은 **설계만 열어두고 구현하지 않음**


※ 본 프로젝트의 로그인/회원가입은 **보안 목적이 아닌 구조·흐름 검증용 데모 구현**이다.


---

## 5. 관리자 기능을 구현하지 않은 이유

- 인증/권한/감사 기준이 완전히 정리되기 전 단계
- 관리자 기능은 복잡도가 급격히 증가
- 현재 목적은 “기능 나열”이 아닌 “구조 검증”


따라서 관리자 영역은 **폴더 및 문서 수준에서만 정의**한다.


---

## 6. 향후 확장 계획

- JSON → REST API → DB 전환
- Spring Boot + MyBatis 연계
- 관리자 페이지 구현
- 금융권 게시판 도메인 구조 연습
- 감사 로그 / 이력 관리 고도화
- 실제 인증 서버 연동


---

## 정리

이 프로젝트는 “완성형 서비스”가 아니라
**금융권 기준으로 설계 사고를 검증하기 위한 최소 단위 구현(MVP)** 이다.



---

## 7. Spring 전환 시 폴더 매핑 전략

본 프로젝트는 순수 HTML / CSS / JS 기반이지만,  
**Spring MVC 구조로의 전환을 전제로 폴더 및 도메인을 분리**하여 설계하였다.

현재 프론트엔드 구조는 Spring Boot 환경으로 거의 그대로 매핑 가능하다.

---

### 7-1. 폴더 매핑 표

| 현재 구조 | Spring Boot 전환 |
|---|---|
| `js/core/storage.js` | Repository / Mapper |
| `js/auth/auth.js` | AuthService |
| `js/auth/guard.js` | Interceptor / AOP |
| `js/auth/user.store.js` | UserRepository |
| `js/board/*.js` | BoardService |
| `auth/*.html` | `templates/auth/*.html` |
| `board/*.html` | `templates/board/*.html` |
| `constants.js` | Enum / Code Table |
| `seed/*.js` | DataInitializer |
| `schema/erd.png` | DB ERD |

---

### 7-2. Spring 패키지 구조 예시

```text
kr.co.bnk.board
├─ controller
│  ├─ AuthController
│  └─ BoardController
├─ service
│  ├─ AuthService
│  └─ BoardService
├─ repository
│  ├─ UserRepository
│  └─ BoardRepository
├─ domain
│  ├─ User
│  └─ Board
└─ common
   ├─ AuthInterceptor
   └─ Constants
```
---

### 7-3. 설계 의도

“프론트엔드 단계에서부터
auth / board / core 도메인을 분리해 구조를 설계했기 때문에
Spring으로 전환하더라도 구조를 거의 그대로 가져갈 수 있습니다.”


