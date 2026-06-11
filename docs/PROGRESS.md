# PROGRESS

## 지금 (Now)

레포 최초의 영속 도구 **토론 리뷰 세트**를 `.claude/`에 추가함 — 에이전트 3개(`design-reviewer` 품질 판정관 / `design-advocate` 구현자 / `design-arbiter` 심판) + 진입점 **skill `design-debate`**(자동 트리거 — "토론해봐" 등 자연어에 발동). 목적: 감사/검증의 확증편향과 구현 드리프트를 *양쪽 동시에* 잡고, 제약으로 "유지" 판정된 건을 **ADR 씨앗**으로 산출(= CLAUDE.md "ADR — 폐기한 길과 이유"의 실행 도구).

**배선을 B(리뷰→토론)로 재구성함** (2026-06-11). 처음엔 A(독립 병렬+심판)로 만들어 end-to-end 1회 검증(general-purpose 폴백, 판정 "과설계 아님")하고 **A 상태를 `cc7cab1`로 커밋**했으나 — 사용자 의도("리뷰어가 먼저 리뷰하고 그 내용을 구현자와 토론")와 A의 "독립 병렬, advocate가 발견사항 안 봄"이 어긋남을 확인. **B로 전환**: 리뷰어 블라인드 선리뷰 → 구현자(advocate)가 각 발견에 동의/제약/반론으로 직접 응답 → 심판. 리뷰어 초기 독립성은 유지, advocate의 (과한) 블라인드만 제거. `design-advocate`·`SKILL.md` 주 변경, `design-arbiter` 정합 수정. **정적 검증 통과(프론트매터·B 표현). 단 B 흐름 end-to-end는 아직 미실행.**

## 다음 (Next)

- **▶ 새 세션에서 `design-debate` 검증** — `docs/runbooks/01-validate-design-debate.md` 절차대로 실행: ①등록 probe(named 호출·skill 자동발동) ②B 흐름 e2e(리뷰→구현자 응답→심판 직렬) ③트리거 오발동 점검. (현 세션은 커스텀 타입 미등록이라 폴백만 가능했음 — 사용자가 Claude Code 재시작 후 진행키로 함.) 통과 시 이 항목 닫고 `human/harness-journal.md`에 한 줄.
- 새 세션에서 실제 코딩 작업을 진행하며 하네스 동작을 관찰하고, `human/harness-journal.md`의 실험 일지 표에 기록한다.
- (보류 중) `README.md` 헤더 재정의 적용 여부 결정 — "하네스 자체가 아니라 그 위에 얹는 협업 규칙 레이어"로 위치를 명확히 하는 안을 **제안만 한 상태(미승인).**

## 미결 (Open / TBD)

- ~~**가 vs 나**~~ → **닫힘: 나(가드레일) 채택** (2026-06-11). 영속 스킬·커맨드·서브에이전트·도구를 AI가 직접 구현하고 통보; 근거 분명할 때만(반복/효율/계획). CLAUDE.md 반영 완료, 저널 4번 참조.
- README 헤더 재정의안 승인/반려.
- 레포 이름: `coding-agent-harness` 유지 vs 대안(`-ext`, `-playbook` 등) — 현재 유지로 기움.
