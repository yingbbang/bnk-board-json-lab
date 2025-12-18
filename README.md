# BNK-BOARD-JSON-LAB

순수 **HTML / CSS / JavaScript** 환경에서  
**게시판 UI + JSON 기반 데이터 시딩(seed) 실험**을 위한 레포지토리이다.

Spring / DB 이전 단계에서  
- 데이터 구조 설계
- 게시판 도메인 분리
- 시드 데이터 관리 방식  
을 검증하는 목적의 실험용 프로젝트다.

### 작업기간
2025.12.18(1일, 11:00~16:00, 점심시간은 작업하지 않음)

---
<br>

### index.html (list) ## 이미지를 누르면 해당 페이지로 이동합니다.
<a href="https://yingbbang.github.io/bnk-board-html/board/index.html"> 
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/snapshot-index.png"></a>

### view.html (view)
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/snapshot-view.png">

### write.html (write) ## 이미지를 누르면 해당 페이지로 이동합니다.
<a href="https://yingbbang.github.io/bnk-board-html/board/write.html"> 
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/snapshot-write.png"></a>

### edit.html (edit)
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/snapshot-edit.png">

### delete.html (delete)
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/snapshot-delete.png">

### ERD
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/erd.png">

### data-dictionary
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/data-dictionary.png">

### code-definition
<img src="https://github.com/yingbbang/bnk-board-html/blob/main/board/assets/dummy/code-definition.png">


## 1. 프로젝트 목적

- 프레임워크 없이 게시판 기능 구현
- 게시글 데이터를 JSON 파일 기반으로 로딩
- 금융권 게시판 도메인 구조 연습
- 추후 Spring + DB 전환을 고려한 구조 검증
- 
---

## 2. 전체 폴더 구조

 
```text
BNK-BOARD-JSON-LAB
├─ board/
│ ├─ assets/
│ │ ├─ banner/ # 배너 이미지
│ │ ├─ css/ # 공통 / 게시판 CSS
│ │ ├─ dummy/ # 설계 참고용 이미지·텍스트
│ │ └─ icons/ # 아이콘 SVG
│ │
│ ├─ js/
│ │ ├─ board_list.js # 게시글 목록
│ │ ├─ board_view.js # 게시글 상세
│ │ ├─ board_write.js # 게시글 작성
│ │ ├─ board_edit.js # 게시글 수정
│ │ ├─ board_delete.js # 게시글 삭제
│ │ ├─ storage.js # localStorage 기반 가상 DB
│ │ └─ util.js # 공통 유틸
│ │
│ ├─ json/
│ │ ├─ notice.json
│ │ ├─ faq.json
│ │ ├─ qna.json
│ │ ├─ it.json
│ │ ├─ security.json
│ │ ├─ finance_product.json
│ │ ├─ pension.json
│ │ ├─ retail.json
│ │ ├─ corporate.json
│ │ ├─ csr.json
│ │ └─ digital_asset.json
│ │
│ ├─ schema/
│ │ ├─ data-dictionary.html # 데이터 사전
│ │ ├─ code-definition.html # 코드 정의서
│ │ └─ erd.png # ERD
│ │
│ ├─ seed/
│ │ └─ board/
│ │ ├─ *.json # 게시판별 시드 데이터
│ │ └─ index.js # 시드 로딩 스크립트
│ │
│ ├─ index.html # 게시글 목록
│ ├─ view.html # 게시글 상세
│ ├─ write.html # 게시글 작성
│ ├─ edit.html # 게시글 수정
│ ├─ delete.html # 게시글 삭제
│ └─ audit.html # 감사/확인용 화면
│
└─ README.md

---

## 3. 주요 디렉토리 설명

### `/board/js`
- 게시판 핵심 로직
- `storage.js`는 localStorage를 **가상 DB**처럼 사용
- 화면 단위 기능을 파일 단위로 명확히 분리

### `/board/json`
- 도메인별 게시글 데이터 원본
- DB 이전 시 테이블 단위 데이터로 전환 가능하도록 설계

### `/board/seed/board`
- JSON → localStorage 초기 적재 실험 영역
- 필요한 JSON만 선택 로딩 가능
- 운영 데이터와 실험 데이터를 명확히 분리

### `/board/schema`
- ERD, 데이터 사전, 코드 정의서
- 설계 의도를 코드와 분리해 문서로 관리

---

## 4. 설계 특징
- 물리 삭제가 아닌 상태값 기반 설계 전제
- 게시판 유형 / 카테고리 분리 구조
- 프론트엔드 단에서도 금융권 도메인 구조 연습
- 즉시 Spring으로 가지 않고 데이터 흐름을 먼저 통제

---

## 5. 향후 확장 계획

- JSON → REST API → DB 전환
- Spring Boot + MyBatis 연계
- 권한(Role) 기반 화면 분기
- 감사 로그 / 이력 관리 고도화

# bnk-board-json-lab
