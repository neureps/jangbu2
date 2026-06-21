---
name: reference-jangbu-logic
description: jangbu.html 내 회계/세무 계산 로직의 위치와 방식
metadata:
  type: reference
---

`/Users/cypark/jangbu/jangbu.html` 단일 파일, 총 1073줄, `<script>`는 332줄~.

핵심 함수 위치(현재 버전):
- `ACCT_TYPE` (334줄): 계정명→분류. 감가상각누계액='자산'(차감), 예수금='부채' 추가됨.
- `NO_VAT_DEDUCT` (346줄): 접대비·차량유지비·차량운반구 매입세액 불공제 → 원가산입.
- `TYPES` (355줄): 거래유형별 분개. 영세율(zero), 급여원천징수(wh→예수금), 예수금납부, 법인카드대금결제 추가.
- `accountBalances(Y)` (627줄): 손익=당해연도만, BS=누적.
- `priorRetained(Y)` (639줄): 전기말 누적손익→전기이월이익잉여금(시산표 자본 보충).
- `accumThrough/depForYear` (747·753줄): 정액·월할 감가상각. monthsHeld=(year-acqYear)*12+(13-acqMonth). 검증결과 월할·잔존0·누계≤원가 정확.
- `buildDepEntry` (758줄): 12/31자 (차)감가상각비/(대)감가상각누계액. dep플래그로 중복방지.
- `renderVat` (824줄): 과세매출(salesTax)/영세율(salesZero) 분리집계. 영세율은 0원 거짓경고 제외.

검증 완료(정확): 감가상각 월할계산, 시산표 차대일치(priorRetained 보충 정확), 영세율 분리집계, 원천징수 예수금 부채처리, 새 비용의 당해손익 반영.

남은 잠재 위험:
- ACCT_TYPE 미등록 계정('기타') 생기면 priorRetained 누락→시산표 불일치(현재는 모두 등록돼 안전).
- 감가상각 [반영] 후 원거래 삭제해도 dep분개 안 지워짐(고아 분개).
- depForYear는 매년 수동반영 필요. 미반영 연도 손익 과대.
- 법인세 산출(과표/세율/세액공제/최저한세) 여전히 전무. 부가세까지만.
- 가지급금인정이자·접대비한도·기부금한도·임원상여한도 등 세무조정 전무(앱이 명시적으로 고지함).
