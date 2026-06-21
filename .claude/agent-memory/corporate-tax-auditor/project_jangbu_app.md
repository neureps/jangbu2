---
name: project-jangbu-app
description: jangbu.html — 소규모 법인용 단일 HTML 복식부기 장부/부가세 집계 웹앱의 목적과 범위
metadata:
  type: project
---

`/Users/cypark/jangbu/jangbu.html` 는 단일 HTML 파일 웹앱.

대상 사용자: 비전문가(소규모 법인 사장님 2명). 12월 결산 법인 가정.
목적: 거래 입력 → 자동 분개(복식부기) → 부가세 분기 집계 → 신고 캘린더. **최종 목적은 법인세 신고 준비**.

**Why:** 세무사 없이 직접 장부를 만들어 법인세 신고를 준비하려 함.
**How to apply:** 법인세 산출(과세표준/세율/세액공제/최저한세) 로직은 현재 전혀 없음 — 부가세까지만 집계. 결산조정/세무조정/감가상각/접대비한도 등도 없음. 검토 시 "누락된 법인세 필수 데이터"를 우선 지적.

데이터 저장: localStorage + File System Access API(암호화 공유파일, 2명 동기화). 회계연도 개념 없이 전체 거래 누적.
