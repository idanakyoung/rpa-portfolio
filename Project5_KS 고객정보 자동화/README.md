Project5_KS 고객정보 자동화/README.md
# 프로젝트 5. KS 고객정보 조회 및 거래 검증 자동화

## 📌 프로젝트 개요

본 프로젝트는 ACME 웹사이트 및 데스크탑 응용프로그램을 활용하여  
고객정보 및 거래 데이터를 수집, 검증, 비교, 기록하는 End-to-End 자동화 프로세스입니다.  
스크래핑 및 검증 결과는 리포트 파일로 정리되며, 시스템 내 Work Item에도 자동 반영됩니다.

---

## 🎯 과제 정보

- **과제명**: KS 고객 거래 데이터 검증 및 리포트 자동화  
- **담당 부서**: 고객관리팀  
- **수행 주기**: 요청 시 수시 실행  
- **수행 방식**: Config 및 사용자 입력 기반 자동화

---

## 🛠 사용 기술

- **UiPath**: 웹 자동화, 데스크탑 UI 자동화, 정규식 기반 텍스트 추출  
- **Excel**: 거래 내역 정리, 리포트 자동 생성  
- **대상 시스템**:  
  - [ACME 웹사이트](https://acme-test.uipath.com)  
  - ACME System3 (데스크탑 응용프로그램)

---

## 🔄 고객정보 검증 워크플로우

| 단계 | 설명 |
|------|------|
| ✅ **STEP 1. WIID 목록 조회** | Type = W1, Status = Open 조건으로 필터링 |
| ✅ **STEP 2. 상세 페이지 정보 추출** | Client ID, Account Number, Amount 정규식 추출 |
| ✅ **STEP 3. 응용프로그램에서 고객조회** | Client ID 기반 검색 후 고객계정 접근 |
| ✅ **STEP 4. 거래 내역 추출 및 계산** | 거래 목록 스크래핑 후 총합 계산 |
| ✅ **STEP 5. Amount 비교 및 검증 결과 생성** | 일치 여부 “O”, “X”로 표시 |
| ✅ **STEP 6. 리포트 저장 및 시트 처리** | 기존 시트 삭제 후 새 리포트 생성 |
| ✅ **STEP 7. Work Item 상태 업데이트** | Status → Completed, Comment 자동 입력 |

---

## 💻 사용 환경

- 운영체제: Windows 10 / 11  
- UiPath Studio: 2023.10.3  
- 대상 시스템:  
  - ACME 웹사이트  
  - ACME System3 (데스크탑 프로그램)

---

## 🔧 사전 준비 사항

- `Config.xlsx` 파일 내 다음 항목 설정 필수:  
  `ACME_URL`, `ACME_ID`, `ACME_PW`, `SourceData`, `Result`, `TemplatePath` 등  
- Credential Manager에 `ACME_ID`, `ACME_PW` 등록  
- 응용프로그램은 실행 가능 상태여야 하며 Client 메뉴 접근 가능  
- 템플릿, 저장 폴더 등 외부 리소스 사전 존재 확인 필요

---

## 📦 사용된 패키지

- UiPath.Credentials.Activities = 2.1.0  
- UiPath.Excel.Activities = 2.22.3  
- UiPath.Mail.Activities = 1.21.1  
- UiPath.System.Activities = 23.10.3  
- UiPath.Testing.Activities = 23.10.0  
- UiPath.UIAutomation.Activities = 23.10.7

---

## 📌 자동화 특징 및 기술 포인트

- 정규표현식 + `Get Full Text` 조합으로 Client 정보 정확히 추출  
- 거래내역 `.Split(vbTab)` → `.AsEnumerable().Sum(...)`로 합산 처리  
- 일치 여부를 "O"/"X"로 구분하여 리포트 작성  
- 기존 파일/시트 존재 시 삭제 후 새로 저장하여 일관성 유지  
- 거래 유형(Online, Offline) 구분 합계도 별도 변수로 저장 가능  
- 결과는 리포트화되고, Work Item에는 상태 및 Comment 자동 반영  
- Config 기반 유연 설계 → 연도, 경로 변경에 강함

---

https://www.notion.so/Project5-KS-20c4bbd537c980a39fa2dd5e9c823f3e?source=copy_link

📁 전체 실행 파일, 결과 예시 및 시연 영상은 추후 GitHub에 업데이트될 예정입니다.

> 작성자: 구나경  
> 이메일: 2215486@donga.ac.kr  
> LinkedIn: [https://www.linkedin.com/in/나경-구-b250b636a/](https://www.linkedin.com/in/%EB%82%98%EA%B2%BD-%EA%B5%AC-b250b636a/)  
> 작성일: 2025년 6월 기준

---
