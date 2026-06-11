# 01 · design-debate 검증 런북

`design-debate` 토론 세트(에이전트 3개 + skill)를 **새 세션에서** 검증하는 재현 가능한 절차.
배경: 커스텀 에이전트/스킬은 세션 시작 시 `.claude/`를 로드할 때만 등록된다. 만든 세션에서는
`subagent_type` 직접 호출과 skill 자동발동이 안 되므로(폴백만 가능), 아래는 **새 세션**에서 돌린다.

## 사전: 등록 확인

1. 새 세션에서 사용 가능한 에이전트 목록에 `design-reviewer` / `design-advocate` / `design-arbiter`가 있는지 확인.
2. `/design-debate`가 슬래시 커맨드로 뜨는지, "이거 토론해봐" 류 자연어에 skill이 자동발동하는지 확인.
   - 안 뜨면: 등록 실패 → 프론트매터·파일 위치(`.claude/agents/*.md`, `.claude/skills/design-debate/SKILL.md`) 점검.

## 1. 등록 probe (가벼움)

각 에이전트를 trivial 작업으로 1회씩 호출해 `subagent_type`이 해석되는지만 본다:
- `design-reviewer`에 "정확히 이 한 줄만 출력: 등록됨" → 정상 반환되면 등록 OK.
- advocate·arbiter도 동일.

## 2. B 흐름 end-to-end (핵심)

작은 실제 대상(예: 이 레포의 `.claude/` 세트 자신, 또는 임의의 소규모 변경)으로 `/design-debate` 실행.
**확인할 것 — 직렬 대화가 의도대로 도는가:**
- [ ] `design-reviewer`가 **변호 입력 없이 블라인드로 먼저** 리뷰하고 잘된점+발견사항(P1~P3)을 냄.
- [ ] `design-advocate`가 그 **발견사항을 받아** 각 건에 동의/제약/반론으로 **직접 응답**(증거 동반)함 — 블라인드 복원이 아니라 발견 앵커된 응답인지.
- [ ] `design-arbiter`가 **발견+응답 쌍**을 항목별 판정(고친다/유지+ADR씨앗/바꾼다)함.
- [ ] 최종 보고에 잘된점·변경목록·ADR 씨앗·다음행동이 다 나옴.
- [ ] 사소한 대상엔 "토론 불필요"로 가볍게 처리하는 적응 동작(SKILL 적응 절)도 한번 확인.

## 3. 트리거 오발동 점검 (P3)

`SKILL.md` description의 예시 문구 7개가 **과하게 자동발동**하는지 실제 사용에서 관찰.
무관한 요청에 자꾸 뜨면 description 예시를 축약한다.

## 결과 기록

- 통과/실패를 `human/harness-journal.md` 실험 일지 표에 한 줄 남기고, `docs/PROGRESS.md` "다음"의 검증 항목을 닫는다.
- B 로직 결함 발견 시: advocate(응답 형식)·SKILL(절차)·arbiter(판정) 중 해당 파일만 수정 후 재검증.
