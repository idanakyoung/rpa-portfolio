Project4_ACME WI4 리포트 자동화/README.md
# 프로젝트 4. ACME WI4 리포트 다운로드 및 자동 보고

## 📌 프로젝트 개요

본 프로젝트는 ACME 시스템에 등록된 WI4 유형의 Open 상태 Work Item을 조회하여  
각 항목의 상세 페이지에 접속한 후 Vendor 관련 정보(TaxID, Name 등)를 추출합니다.  
TaxID를 기준으로 월별 리포트를 다운로드하고, 연간 단일 Excel 파일로 병합한 뒤 업로드합니다.  
업로드 완료 후에는 시스템에서 제공하는 Confirmation ID를 해당 Work Item에 반영하고,  
최종 결과는 지정된 템플릿 형식의 엑셀 보고서로 정리됩니다.

---

## 🎯 과제 정보

- **과제명**: ACME WI4 리포트 자동 수집 및 등록  
- **담당 부서**: 운영관리팀  
- **수행 주기**: 분기별 / 요청 시  
- **수행 방식**: Config 기반 End-to-End 자동화

---

## 🛠 사용 기술

- **UiPath**: 웹 UI 자동화, 정규표현식 추출, CSV 병합, 파일 업로드/다운로드  
- **Excel**: 월별 리포트 병합, 템플릿 기반 최종 결과 정리, 매크로 자동 실행  
- **대상 시스템**: [ACME 테스트 사이트](https://acme-test.uipath.com)

---

## 🔄 자동화 워크플로우

| 단계 | 설명 |
|------|------|
| ✅ **STEP 0. 프로세스 초기화** | Chrome 및 Excel 프로세스 종료로 충돌 방지 |
| ✅ **STEP 1. Config 로드** | 다중 시트 구성 Config.xlsx 로드 및 Dictionary 구성 |
| ✅ **STEP 2. ACME 로그인** | Credential 기반 로그인, 기존 세션 로그아웃 처리 포함 |
| ✅ **STEP 3. WorkItems 조회 및 필터링** | WI4 + Open 조건 필터, `DT_WI4OpenItems` 생성 |
| ✅ **STEP 4. 상세 정보 추출** | WIID별 TaxID, VendorName 등 정규식 추출 |
| ✅ **STEP 5. 월별 리포트 다운로드** | TaxID 기준 월별 리포트 자동 저장, 예외 메시지 대응 |
| ✅ **STEP 6. 연간 엑셀 병합** | CSV 병합 후 `.xlsx` 저장, 컬럼 구조 유연 대응 |
| ✅ **STEP 7. 엑셀 업로드 및 Confirmation 추출** | 업로드 성공 시 Confirmation ID 추출 및 저장 |
| ✅ **STEP 8. WorkItems 상태 업데이트** | 상태 변경: Completed, Comment에 Confirmation ID 입력 |
| ✅ **STEP 9. 결과 엑셀 정리** | 템플릿 복사 후 시트명 변경, 최종 보고서 작성

---

## 💻 사용 환경

- 운영체제: Windows 10 / 11  
- UiPath Studio: 2023.10.3  
- 대상 사이트: [https://acme-test.uipath.com](https://acme-test.uipath.com)

---

## 🔧 사전 준비 사항

- `Config.xlsx` 파일 경로 및 다음 Key 값들이 정확히 세팅되어 있어야 함  
  (예: `System1_URL`, `System1_Account`, `DownloadMonthlyReportURL`,  
  `UploadYearlyReportURL`, `YearlyReport`, `TemplatePath`, `ResultPath`, `RenameSheetMacro` 등)  
- Credential 저장소에 `System1_Account` 자격 증명 등록  
- 템플릿 파일과 결과 저장 경로가 사전에 존재해야 하며, 덮어쓰기 가능 권한 필요  
- 로그인 정보(`Str_ACME_ID`, `Str_ACME_PW`) 정확히 기입 필요

---

## 📦 사용된 패키지

- UiPath.Excel.Activities = 22.2.3  
- UiPath.Mail.Activities = 1.21.1  
- UiPath.System.Activities = 23.10.3  
- UiPath.Testing.Activities = 23.10.0  
- UiPath.UIAutomation.Activities = 23.10.7

---

## 📌 자동화 특징 및 기술 포인트

- Config 기반 동적 변수 관리로 유지보수 편의성 향상  
- WI4 + Open 조건 필터 및 정규식 기반 데이터 수집  
- TaxID별 리포트 저장 구조 자동 생성 및 중복 방지  
- `.Clone()` 방식으로 병합 시 컬럼 구조 불일치 대응  
- Confirmation ID 자동 파싱 후 DataTable 및 시스템 반영  
- 매크로 호출을 통한 시트명 자동 정리  
- 전 구간 자동화 구성으로 수작업 없는 End-to-End 처리  
- 연도 변경 및 경로 수정은 Config에서만 조정 가능

---

## 📁자세한 설계 흐름 및 액티비티 속성 설명
👉 [Notion 포트폴리오에서 확인하기](https://www.notion.so/Project4-ACME-WI4-20c4bbd537c980239c8bc4886045f447?source=copy_link)

--- 

📁 전체 소스 코드 및 샘플 결과물은 추후 GitHub에 업로드될 예정입니다.

> **작성자**: 구나경  
> **이메일**: 2215486@donga.ac.kr  
> **LinkedIn**: [나경 구 - LinkedIn](https://www.notion.so/Project4-ACME-WI4-20c4bbd537c980239c8bc4886045f447?source=copy_link)  
> **작성일**: 2025년 7월 기준

