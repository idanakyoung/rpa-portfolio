Project3_ACME 인보이스 자동 다운로드/README.md
# 프로젝트 3. ACME 인보이스 자동 다운로드 및 Total 값 검증

## 📌 프로젝트 개요

본 프로젝트는 사용자가 선택한 Vendor ID와 검증 대상 월(Month)을 기준으로  
ACME 시스템에서 월별 인보이스 파일을 자동 다운로드하고,  
기준 엑셀 파일의 Total 값과 비교하여 **정합성을 검증**하는 자동화 프로세스입니다.

모든 검증 결과는 ‘ACME Total’, ‘검증’, ‘오류 원인’ 열에 자동 기록되며,  
최종 결과는 엑셀 저장 및 이메일 발송 기능을 통해 공유할 수 있습니다.

---

## 🎯 과제 정보

- **과제명**: ACME 인보이스 다운로드 및 검증 자동화  
- **담당 부서**: 회계팀  
- **수행 주기**: 월별 (또는 수시 요청 시)  
- **수행 방식**: 사용자 입력 기반 자동화

---

## 🛠 사용 기술

- **UiPath**: 웹 자동화, 엑셀 비교, 조건 검증, 메일 발송  
- **Excel**: Total 값 기준 비교 및 자동 정리  
- **대상 웹사이트**: [https://acme-test.uipath.com](https://acme-test.uipath.com)

---

## 🔄 인보이스 검증 워크플로우

| 단계 | 설명 |
|------|------|
| ✅ **STEP 1. 변수 및 경로 초기화** | 엑셀 경로, Vendor ID, Month 등 입력값 초기화 |
| ✅ **STEP 2. 사용자 입력 수집** | Vendor 선택, 월 입력 (쉼표 구분 숫자 입력) |
| ✅ **STEP 3. ACME 사이트 접속 및 로그인** | 사이트 접속, 로그인 ID/PW 입력 |
| ✅ **STEP 4. 인보이스 다운로드** | 선택된 Vendor/Month 조합별 파일 다운로드 |
| ✅ **STEP 5. ACME Total 계산** | 각 파일의 Total 값을 합산하여 계산 |
| ✅ **STEP 6. 정합성 검증 및 결과 기록** | 기준 엑셀과 비교 후 결과 자동 입력 |
| ✅ **STEP 7. 결과 파일 저장 및 메일 전송** | 결과 정리 후 저장 / 메일로 전송

---

## 💻 사용 환경

- 운영체제: Windows 10 / 11  
- UiPath Studio: 2023.10.3  
- 대상 웹사이트: [https://acme-test.uipath.com](https://acme-test.uipath.com)

---

## 🔧 사전 준비 사항

- 기준 엑셀 파일(`Full_Invoice_Report_ADVANCED.xlsx`)이 미리 존재해야 함  
- `Str_SourcePath`, `Str_ResultPath`, `Str_FullFilePath` 등 변수 사전 설정 필수  
- Vendor ID 입력 방식은 **1:N** 또는 **N:N** 구조 중 선택 가능  
- 검증할 월(Month)은 쉼표로 구분된 숫자로 입력 (예: `1,2,3`)  
- ACME 로그인 정보(`Str_ACME_ID`, `Str_ACME_PW`)가 정확해야 하며, 사전 가입 필요

---

## 📦 사용된 패키지

- UiPath.Excel.Activities = 22.2.3  
- UiPath.Mail.Activities = 1.21.1  
- UiPath.System.Activities = 23.10.3  
- UiPath.Testing.Activities = 23.10.0  
- UiPath.UIAutomation.Activities = 23.10.7

---

## 📌 자동화 특징 및 예외 처리

- 🔁 각 Vendor × 월 조합으로 반복 처리  
- 🗃️ 동일 파일 존재 시 삭제 후 재다운로드  
- 📉 Total 값을 합산하고 ±0.001 이내면 "O", 아니면 "X"로 검증  
- ❗ ACME Total 값 없음, 파일 누락 시 → "엑셀 다운로드 실패" 또는 빈 셀 처리  
- 📊 엑셀 결과에 `ACME Total`, `검증`, `오류 원인` 자동 입력  
- 📁 저장 파일명 규칙: `Report-{Vendor}-{Month}.xlsx`  
- 📧 결과 파일 메일 전송 기능 포함 (Outlook 또는 SMTP 설정 필요)  
- 💥 ACME 사이트 중복 실행 시 `Kill Process`로 사전 종료

---

## 📁자세한 설계 흐름 및 액티비티 속성 설명
👉 [Notion 포트폴리오에서 확인하기](https://www.notion.so/Project3-ACME-20c4bbd537c980428d28ff455e2e09f6?source=copy_link)

--- 

📁 전체 소스 파일 및 시연 영상은 추후 GitHub에 업데이트될 예정입니다.

> 작성자: 구나경  
> 이메일: 2215486@donga.ac.kr  
> LinkedIn: [https://www.linkedin.com/in/나경-구-b250b636a/](https://www.linkedin.com/in/%EB%82%98%EA%B2%BD-%EA%B5%AC-b250b636a/)  
