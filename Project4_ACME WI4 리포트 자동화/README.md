Project4_ACME WI4 리포트 자동화/README.md
# 프로젝트 4. ACME WI4 리포트 다운로드 및 자동 보고

## 📌 프로젝트 개요

본 프로젝트는 ACME 시스템에서 WI4 유형의 Open 상태 Work Item을 조회하여  
각 항목의 TaxID 정보를 기준으로 월별 리포트를 다운로드하고, 연간 단일 Excel로 병합 후 업로드합니다.  
업로드 완료 후에는 시스템으로부터 받은 Confirmation ID를 해당 Work Item에 자동 반영하고,  
최종 결과는 지정된 템플릿 형식의 보고서로 정리됩니다.

---

## 🎯 과제 정보

- **과제명**: ACME WI4 리포트 자동 수집 및 등록  
- **담당 부서**: 운영관리팀  
- **수행 주기**: 분기별 / 요청 시  
- **수행 방식**: Config 기반 End-to-End 자동화

---

## 🛠 사용 기술

- **UiPath**: 웹 UI 자동화, 엑셀 병합 및 업로드, 정규식 추출  
- **Excel**: 월별 리포트 병합, 템플릿 기반 최종 결과 정리  
- **대상 시스템**: [ACME 테스트 사이트](https://acme-test.uipath.com)

---

## 🔄 자동화 워크플로우

| 단계 | 설명 |
|------|------|
| ✅ **STEP 1. WI4 WorkItem 조회** | Config 기준 (Type = WI4, Status = Open) 필터링 |
| ✅ **STEP 2. 상세 페이지 정보 추출** | TaxID, Name, Address 등 정규식 기반 추출 |
| ✅ **STEP 3. TaxID 기준 리포트 다운로드** | 월별 보고서 자동 다운로드 (중복 방지 포함) |
| ✅ **STEP 4. 연간 엑셀 병합 처리** | .Clone() 구조 병합, 컬럼 유연성 확보 |
| ✅ **STEP 5. 리포트 업로드 및 확인 ID 추출** | Upload 후 반환되는 Confirmation ID 기록 |
| ✅ **STEP 6. WorkItem 상태 업데이트** | 결과 반영 후 최종 보고 템플릿 정리 |

---

## 💻 사용 환경

- 운영체제: Windows 10 / 11  
- UiPath Studio: 2023.10.3  
- 대상 사이트: [https://acme-test.uipath.com](https://acme-test.uipath.com)

---

## 🔧 사전 준비 사항

- `Config.xlsx` 파일 존재 및 Key 값 정확하게 설정 필요  
  (예: `System1_URL`, `YearlyReport`, `RenameSheetMacro`, `ResultPath` 등)  
- Credential 저장소에 `System1_Account` 자격 증명 등록 필수  
- 템플릿 파일(`TemplatePath`)과 결과 저장 경로 미리 생성되어 있어야 함  
- 기존 파일 덮어쓰기 또는 삭제 권한 필요  
- 로그인 정보(`Str_ACME_ID`, `Str_ACME_PW`) 사전 확인

---

## 📦 사용된 패키지

- UiPath.Excel.Activities = 22.2.3  
- UiPath.Mail.Activities = 1.21.1  
- UiPath.System.Activities = 23.10.3  
- UiPath.Testing.Activities = 23.10.0  
- UiPath.UIAutomation.Activities = 23.10.7

---

## 📌 자동화 특징 및 기술 포인트

- Config 기반 구조 설계로 유지보수 편의성 확보  
- TaxID 기반 폴더 생성 및 파일 중복 방지  
- 월별 CSV 파일 병합 시 컬럼 차이 자동 대응 (`.Clone()` 방식)  
- Confirmation ID 파싱 후 자동 반영  
- End-to-End 자동화 구성으로 작업자 수작업 제거  
- 연도 변경 및 경로 변경 시 Config만 수정하면 재사용 가능

---

📁 전체 소스 코드 및 실행 결과 샘플은 추후 GitHub에 업로드될 예정입니다.

> 작성자: 구나경  
> 이메일: 2215486@donga.ac.kr  
> LinkedIn: [https://www.linkedin.com/in/나경-구-b250b636a/](https://www.linkedin.com/in/%EB%82%98%EA%B2%BD-%EA%B5%AC-b250b636a/)  
> 작성일: 2025년 6월 기준

---
