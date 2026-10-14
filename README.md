# 업무 자동화 프롬프트 패키지 — 회의록 요약 봇 "미닛"

LLM 3종을 같은 회의록 요약 과업으로 비교해 하나를 고르고, 페르소나, 시스템 프롬프트, Few-shot, 단계적 추론, 환각 검증을 적용해 개선한 프롬프트 패키지입니다.

## 산출물

| 산출물 | 파일 |
|---|---|
| ① LLM 모델 비교·선정 보고서 | [`docs/01_model_comparison.md`](docs/01_model_comparison.md) |
| ② 시스템 설계 문서 | [`docs/02_system_design.md`](docs/02_system_design.md) |
| ③ 실행 로그 (12턴 대화) | [`docs/03_conversation_log.md`](docs/03_conversation_log.md) |
| 원본 로그 (전문) | [`logs/raw/`](logs/raw/) |

## 폴더 구조

```
prompts/
  00_meeting_notes.md          테스트 입력(가상 회의 메모) + 정답 키
  01_run_v1.md                 Run A: v1 간단 프롬프트
  02_system_prompt_v2.md       Run B: v2 최종 프롬프트 (페르소나 + 단계적 절차 + Few-shot)
  03_hallucination_questions.md Run C: 환각 검증 질문 7개
  04_conversation_script.md    Run D: 12턴 대화 대본 + 턴별 판정 기준
docs/                          제출 문서 3종
logs/raw/                      모델 응답 원문
```

## 진행 체크리스트

**나** = 직접 할 일 (웹에서 실행·복사) / **Claude** = Claude Code가 할 일

### 0단계: 준비
- [x] **Claude** 업무 과업 정의, 테스트 입력, 정답 키 작성
- [x] **Claude** 페르소나, 시스템 프롬프트 v1/v2, Few-shot 3개 작성
- [x] **Claude** 환각 검증 질문 7개와 판정 기준 작성
- [x] **Claude** 12턴 대화 대본과 턴별 판정 기준 작성
- [ ] **나** 비교할 모델 3개의 웹 계정 준비 (예: ChatGPT, Claude, Gemini)
- [ ] **나** 각 서비스에서 **웹 검색, 메모리, 커스텀 지시 끄기** (공정 비교용)

### 1단계: 모델 비교 (모델마다 반복, 약 10분 × 3)
- [ ] **나** 새 채팅 → `prompts/01_run_v1.md` 박스 붙여넣기 → 응답 복사
- [ ] **나** 새 채팅 → `prompts/02_system_prompt_v2.md`의 `[시스템 지시]` 블록 붙여넣기 → 응답 복사
- [ ] **나** 같은 채팅 → `prompts/03_hallucination_questions.md` 박스 붙여넣기 → 응답 복사
- [ ] **나** 기록: 화면에 표시된 **모델명**, **요금제**, **날짜**, 무료라면 겪은 제한 1줄, 체감 속도
- [ ] **나** 응답을 Claude Code에 붙여넣기 ("ChatGPT Run A:" 처럼 라벨을 붙여서)
- [ ] **Claude** 원본을 `logs/raw/`에 저장하고 정답 키로 채점한 뒤 `docs/01_model_comparison.md` 작성
- [ ] **Claude** v1 vs v2 비교표를 `docs/02_system_design.md` 9장에 작성

### 2단계: 12턴 대화 (선정 모델 1개, 약 20분)
- [ ] **나** 새 채팅에서 `prompts/04_conversation_script.md`의 U1~U12를 순서대로 보내기
- [ ] **나** 대화 전체를 복사해 Claude Code에 붙여넣기 (공유 링크가 있으면 같이)
- [ ] **Claude** 턴별 판정, 문제 지점 분석, `docs/03_conversation_log.md` 작성
- [ ] **Claude** 문제가 있으면 프롬프트 v2.1 수정안 작성 → **나** 해당 턴만 재실행 → **Claude** 결과 기록

### 3단계: 마무리
- [ ] **Claude** 문서 3종의 `{…}` 칸이 남지 않았는지 점검, 개인정보 포함 여부 점검
- [ ] **Claude** 커밋 → **나** push 여부 결정

### 보너스 (선택)
- [ ] 보너스 1: v2 프롬프트를 ChatGPT GPTs, Gemini Gem, Claude Project 중 하나로 배포
- [ ] 보너스 2: 최종 회의 요약을 바탕으로 이미지 생성 AI로 일정·Action Item 인포그래픽 1장 만들기

## 안전·윤리 준수
- 회의 메모는 가상 시나리오이며, 실명 대신 역할명만 사용했습니다.
- 사실·정책·수치 답변에는 "근거 제시 또는 확인 필요" 규칙을 시스템 프롬프트에 넣었습니다.
