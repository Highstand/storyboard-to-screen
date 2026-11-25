# storyboard-to-screen

기획자가 준 화면설계서(스토리보드) PDF에서 출발해, 디자이너가 시안을 만들고 구현 화면까지 검수하는 흐름을 담은 Claude Code 플러그인이에요.

```
화면설계서 PDF ──screen-spec──▶ screen-spec.md ──(디자인·구현)──▶ 피그마 시안 + 구현 화면 ──design-check──▶ 시안·구현 검토.md
```

## 들어 있는 것

| 스킬 | 하는 일 |
|---|---|
| `screen-spec` | 화면설계서 PDF를 읽고 `output/<PDF 파일명>_screen-spec.md`를 만들어요. 화면 목록, 화면별 UI 요소·상태 4종(기본/빈/에러/로딩)·인터랙션·원문 문구, 원본 페이지 번호, 기획자 질문('디자인 전에 꼭 확인' 7건 이하 + '나중에 확인')을 정리해요. |
| `design-check` | screen-spec.md를 기준으로 피그마 시안과 구현 화면을 함께 검수해요. 구현 화면은 로컬 서버에서 직접 눌러보고, 찾은 것을 '고칠 것 · 맞출 것 · 정상(기획 미정)'으로 나눠 `output/<프로젝트명> 시안·구현 검토.md`에 저장해요. |

## 필요한 것

- [Claude Code](https://claude.com/claude-code)
- **Figma 연결** — 이 플러그인에는 Figma 커넥터가 들어 있지 않아요. Figma 공식 플러그인(`figma@claude-plugins-official`)을 설치하거나, claude.ai의 Customize → Connectors에서 Figma를 연결해 두세요. 둘 중 하나만 있으면 돼요.

## 설치

```bash
claude plugin marketplace add Highstand/storyboard-to-screen
```

```bash
claude plugin install storyboard-to-screen@figmatutor
```

## 써 보기

`example/` 폴더에 예시 화면설계서 PDF가 있어요. 작업 폴더에 `storyboard/` 폴더를 만들어 PDF를 넣고 이렇게 말해 보세요.

- "storyboard 폴더의 화면설계서 정리해줘" → `screen-spec`
- "피그마 시안이랑 구현 화면 검토해줘" → `design-check`

## 규칙 요약

- 설계서에 없는 요소·문구·상태는 지어내지 않고 `미정의`로 두고 질문으로 올려요.
- 문구는 원문 그대로 옮겨요.
- '디자인 전에 꼭 확인'은 7건을 넘기지 않아요. 질문 번호는 한 번 붙이면 바꾸지 않아요.
- 검수에서 고치는 건 사용자 승인 뒤에 해요.

## 폴더 구조

```
.claude-plugin/marketplace.json   마켓플레이스(figmatutor)
storyboard-to-screen/             플러그인
  .claude-plugin/plugin.json
  skills/screen-spec/SKILL.md
  skills/design-check/SKILL.md
example/                          예시 화면설계서 PDF
```

## 라이선스

MIT — [LICENSE](LICENSE)
