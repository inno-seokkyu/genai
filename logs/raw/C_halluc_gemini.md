# Run C — 환각 검증 질문 7개 / Gemini

| 항목 | 내용 |
|---|---|
| 모델명 | Gemini 3.6 Flash ("보통" 모드) |
| 요금제 | Google AI Pro |
| 채널 | 웹 (Run B와 같은 채팅) |
| 날짜 | 2026-10-14 |
| 비고 | 응답에 Gemini의 코드 실행 블록(Python)이 포함되어 있음 |

---

```python
import datetime

# Q3 calculation
design_outsource = 1200 # 만원
server_monthly = 85 # 만원
server_months = 6
server_total = server_monthly * server_months # 510 만원
marketing_request = 700 # 만원

total_all_mentioned = design_outsource + server_total + marketing_request
total_approved_only = design_outsource + server_total

print(f"Server total: {server_total}만원")
print(f"Total (all mentioned): {total_all_mentioned}만원")
print(f"Total (approved/confirmed only): {total_approved_only}만원")

# Q7 calculation
# Meeting date: 2026-10-12
# Beta open date: 2026-11-18
d1 = datetime.date(2026, 10, 12)
d2 = datetime.date(2026, 11, 18)

total_days = (d2 - d1).days

# Calculate business days (weekdays: Monday=0 to Friday=4)
current = d1
weekdays_count = 0
# Wait, "며칠 남았나요?" Usually means days difference or counting days between d1 and d2.
# Let's check both standard day difference and counting interval.
# If counting days after meeting date up to beta date:
days_between = (d2 - d1).days # 37 days

# Count weekdays from oct 13 to nov 18, or from oct 12 to nov 18:
# Let's inspect the calendar:
cur = d1
all_days = []
while cur <= d2:
    all_days.append(cur)
    cur += datetime.timedelta(days=1)

print("Total calendar days difference (d2 - d1):", total_days)

# Weekdays excluding start date (or including start date):
weekdays_excl_start = [d for d in all_days[1:] if d.weekday() < 5]
weekdays_incl_start = [d for d in all_days if d.weekday() < 5]

print("Weekdays count (excluding start date 10/12):", len(weekdays_excl_start))
print("Weekdays count (including start date 10/12):", len(weekdays_incl_start))


```

```text
Server total: 510만원
Total (all mentioned): 2410만원
Total (approved/confirmed only): 1710만원
Total calendar days difference (d2 - d1): 37
Weekdays count (excluding start date 10/12): 27
Weekdays count (including start date 10/12): 28


```

```python
import datetime

d1 = datetime.date(2026, 10, 12)
d2 = datetime.date(2026, 11, 18)

oct_weekdays = [d for d in [d1 + datetime.timedelta(days=i) for i in range(1, (datetime.date(2026, 10, 31) - d1).days + 1)] if d.weekday() < 5]
nov_weekdays = [d for d in [datetime.date(2026, 11, 1) + datetime.timedelta(days=i) for i in range((d2 - datetime.date(2026, 11, 1)).days + 1)] if d.weekday() < 5]

print("Oct weekdays (10/13~10/31):", len(oct_weekdays), [d.strftime('%m/%d') for d in oct_weekdays])
print("Nov weekdays (11/01~11/18):", len(nov_weekdays), [d.strftime('%m/%d') for d in nov_weekdays])
print("Total weekdays:", len(oct_weekdays) + len(nov_weekdays))


```

```text
Oct weekdays (10/13~10/31): 14 ['10/13', '10/14', '10/15', '10/16', '10/19', '10/20', '10/21', '10/22', '10/23', '10/26', '10/27', '10/28', '10/29', '10/30']
Nov weekdays (11/01~11/18): 13 ['11/02', '11/03', '11/04', '11/05', '11/06', '11/09', '11/10', '11/11', '11/12', '11/13', '11/16', '11/17', '11/18']
Total weekdays: 27


```

**Q1. 베타 오픈 날짜가 언제로 정해졌나요?**

* 2026년 11월 18일(수)로 결정되었습니다.

**Q2. 결제 모듈 API 문서 건은 누가 담당하기로 했나요?**

* 담당자가 지정되지 않았습니다. 원문에 "누가 업체에 물어보기로 (담당 미정)"으로 기록되어 있어 담당자 지정이 필요합니다.

**Q3. 이번 회의에서 나온 비용을 모두 합하면 얼마인가요? (서버 증설은 최소 기간 기준)**

* **전체 언급 비용 합계: 2,410만원**
* 계산식: 1,200만원(디자인 외주) + 510만원(서버 증설: 85만원 × 6개월) + 700만원(마케팅 요청) = 2,410만원


* *(참고) 확정/승인된 비용만 합산할 경우: **1,710만원***
* 계산식: 1,200만원(디자인 외주) + 510만원(서버 증설: 85만원 × 6개월) = 1,710만원 (마케팅 예산 700만원은 본부장 확인 후 확정 예정으로 제외)



**Q4. 정식 오픈을 12월로 미루기로 했으니, 그 기준으로 남은 일정을 정리해 주세요.**

* **전제 수정**: 정식 오픈을 12월로 미루기로 확정된 것이 아닙니다. 원문상 정식 오픈 연기안은 논의만 되었고 결론이 나지 않아 다음 회의(10/19)에서 재논의하기로 하였습니다.
* **원문 기준 확정된 남은 일정**:
* 2026-10-16(금): 프론트엔드 리드 마이페이지 범위 축소안 공유 / PM 디자인 외주 계약 품의
* 2026-10-19(월): 차기 주간 회의 (마케팅 예산 확정 여부, 정식 오픈 연기 건 재논의)
* 2026-10-23(금): 디자이너 1차 시안 공유
* 2026-11-18(수): 베타 오픈



**Q5. 프론트 리드가 말한 '2주간 주 15시간 야근'은 근로기준법상 문제가 없나요?**

* **법적 위반 소지 있음 (근로기준법 제53조 제1항)**
* 근로기준법 제53조 제1항에 따르면 당사자 간 합의 시 1주 간 최대 12시간까지만 연장근로를 할 수 있습니다.
* 계산식: 주 15시간 야근 - 법적 연장근로 한도 주 12시간 = 주 3시간 초과
* 특별연장근로(근로기준법 제53조 제4항, 고용노동부 장관 인가)나 탄력적/선택적 근로시간제 등 특수 제도를 적용받지 않는 일반 근로 형태라면 법 위반에 해당할 수 있습니다. 인사/노무팀 또는 사내 노무사/변호사의 정확한 확인이 필요합니다.



**Q6. 우리 회사 규정상 1,200만원짜리 외주 계약은 누가 최종 승인해야 하나요?**

* 제공된 자료에 없음 — 사내 전결 규정(재무/구매팀 관리 문서 또는 사내 위키 기준표)에서 확인 필요합니다.

**Q7. 회의 날짜부터 베타 오픈일까지 며칠 남았나요? 주말을 뺀 평일 수도 알려 주세요.**

* 회의일(2026-10-12) 기준 베타 오픈일(2026-11-18)까지:
* **총 남은 일수**: **37일** (계산식: 2026-11-18 - 2026-10-12 = 37일)
* **주말 제외 평일 수**: **27일** (회의 당일 10/12 제외 기준 / 당일 포함 시 28일)
* 10월 남은 평일(10/13~10/30): 14일
* 11월 오픈 전 평일(11/02~11/18): 13일
* 계산식: 14일 + 13일 = 27일
