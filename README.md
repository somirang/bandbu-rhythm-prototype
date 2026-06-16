# 4Key Rhythm Prototype

밴드부 리듬게임 노트 제작 참고용 standalone HTML 프로토타입입니다. 최종 게임이라기보다 노트 타이밍, 밀도, 난이도 곡선, 동시입력, 롱노트, 피버, 입력감, 결과 흐름을 빠르게 확인하는 테스트 툴입니다.

## 실행 방법

1. `index.html`을 브라우저에서 엽니다.
2. 첫 화면에서는 아무 곡도 선택되어 있지 않습니다. `Tutorial`, `ClassRoom`, `Recruitment`, `Main` 중 하나를 클릭해 곡을 고릅니다.
3. 곡을 클릭하면 해당 곡을 짧게 미리 들을 수 있습니다. `Main`은 `Easy / Normal / Hard` 중 난이도를 골라야 시작할 수 있고, 난이도를 바꿔도 같은 메인곡 미리듣기는 처음부터 다시 시작하지 않습니다.
4. 기본 키는 `D / F / J / K`입니다. 시작 전 `KEYS` 영역에서 원하는 키로 바꿀 수 있습니다. `Space`는 사용하지 않습니다.
5. 화면 중앙의 `Start`를 누르면 `READY -> 3 -> 2 -> 1 -> START` 카운트다운과 키 가이드가 나온 뒤 음악과 노트가 시작됩니다.
6. 곡이 끝나면 결과창에서 점수, 최대 콤보, 정확도, 판정 수, Stage Sync, Story Impact, 랭크를 확인할 수 있습니다.
7. 결과창의 `REPLAY`는 같은 곡/난이도를 다시 시작하고, `SELECT SONG`은 새로고침 없이 곡/난이도 선택 화면으로 돌아갑니다.

파일 직접 열기가 막히면 이 폴더에서 로컬 서버로 확인하세요.

```powershell
& "C:\Users\HS\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe" -m http.server 4173
```

그다음 브라우저에서 `http://localhost:4173`을 엽니다.

## 포함 파일

- `index.html`: standalone 실행 파일이며 Tutorial/ClassRoom/Recruitment/Main 차트가 내장되어 있습니다.
- `tutorial.wav`: 첫 곡용 튜토리얼 음악입니다.
- `ClassRoom.wav`: 튜토리얼 다음 단계용 단일 난이도 음악입니다.
- `Recruitment.wav`: 영입 신경전 장면용 단일 난이도 음악입니다.
- `main.wav`: 메인 곡 음악입니다.
- `chart_tutorial_4key.json`: 튜토리얼 차트 원본입니다.
- `chart_classroom_4key.json`: ClassRoom 차트 원본입니다.
- `chart_recruitment_4key.json`: Recruitment 차트 원본입니다.
- `chart_main_4key_easy.json`: Main Easy 차트 원본입니다.
- `chart_main_4key_normal.json`: Main Normal 차트 원본입니다.
- `chart_main_4key_hard.json`: Main Hard 차트 원본입니다.
- `note_chart_tutorial_4key.csv`: 튜토리얼 노트 제작 검토용 CSV입니다.
- `note_chart_classroom_4key.csv`: ClassRoom 노트 제작 검토용 CSV입니다.
- `note_chart_recruitment_4key.csv`: Recruitment 노트 제작 검토용 CSV입니다.
- `note_chart_easy_4key.csv`: Main Easy 노트 제작 검토용 CSV입니다.
- `note_chart_normal_4key.csv`: Main Normal 노트 제작 검토용 CSV입니다.
- `note_chart_hard_4key.csv`: Main Hard 노트 제작 검토용 CSV입니다.
- `assets/ui`: 현재 UI와 노트 참고 에셋입니다.

## 판정 기준

- Perfect: +/-60ms
- Great: +/-110ms
- Good: +/-180ms
- Miss: Good 범위 밖, 노트를 놓친 경우, 롱노트를 너무 일찍 놓친 경우

## 현재 기능

- 4키 기본 입력: `D / F / J / K`
- 시작 전 키 커스터마이징 지원
- 곡 선택: `Tutorial / ClassRoom / Recruitment / Main`
- Main 난이도: `Easy / Normal / Hard`
- Tutorial, ClassRoom, Recruitment는 단일 난이도
- 곡 클릭 미리듣기 지원
- 시작 전 카운트다운, 카운트다운 사운드, 판정선 근처 키 가이드
- 오른쪽에서 왼쪽으로 접근하는 노트
- 단노트, 롱노트, 2키 동시입력 지원
- 인게임 HUD: Combo, Score, Fever/Progress, 판정 팝업
- 결과창: Final Score, Max Combo, Accuracy, Stage Sync, Story Impact, 판정 수, Rank, Replay, Select Song
- 50콤보 단위 콤보 마일스톤 표시
- 입력 tick, 성공 hit, 실패 miss, Fever start 사운드
- 롱노트 hold 중 노트/레인/판정선 glow, pulse, trail 피드백
- Fever Time 중 배경/판정선 pulse, 화면 가장자리 glow, 색감 변화
- Canvas 기반 stage light, hit burst, particle, judgement pop/fade
- 결과 후 새로고침 없이 Replay 또는 곡/난이도 재선택 가능

## 차트 방향

- Tutorial은 약 93 BPM 기준으로 분석한 박자 위상에 맞춰 배치했고, 메인 Easy보다 훨씬 쉽게 설계했습니다.
- Tutorial은 처음 4초 동안 노트가 없고, 이후 `단노트 -> 롱노트 -> 2키 동시입력 -> 종합 복습` 순서로 학습합니다.
- Tutorial의 1/4 구간은 단노트만, 2/4 구간은 롱노트만, 3/4 구간은 2키 동시입력만 사용합니다.
- ClassRoom은 약 103 BPM 기준으로 분석한 정박 위상에 맞춰 배치했고, 마지막 3초 이상은 노트가 나오지 않도록 피날레를 정리했습니다.
- ClassRoom은 처음 4초 동안 노트가 없고, `준비 도입 -> 교실 그루브 -> 빌드업 -> 하이라이트 -> 회복 -> 피날레` 구조로 밀도가 오르내립니다.
- Recruitment는 약 136 BPM 기준으로 분석한 정박 위상에 맞춰 배치했고, ClassRoom과 비슷하거나 아주 약간 더 긴장감 있게 설계했습니다.
- Recruitment는 처음 4초와 마지막 4초 동안 노트가 없고, `질문-답변 -> 밀고 당기기 -> 긴장 상승 -> 협상 하이라이트 -> 회복 -> 결정` 구조로 전개됩니다.
- Main 차트는 100 BPM 기준 2~4마디 단위 반복/변형 루프를 사용합니다.
- JSON/CSV에는 `section`, `pattern`, `intent`가 포함되어 노트 제작 의도를 확인할 수 있습니다.

## 현재 통계

Tutorial:
- 타이밍 이벤트: 42
- 실제 레인 노트: 55
- 동시입력: 13
- 롱노트: 9

ClassRoom:
- 타이밍 이벤트: 89
- 실제 레인 노트: 100
- 동시입력: 11
- 롱노트: 6

Recruitment:
- 타이밍 이벤트: 138
- 실제 레인 노트: 157
- 동시입력: 19
- 롱노트: 5

Main Easy:
- 타이밍 이벤트: 163
- 실제 레인 노트: 173
- 동시입력: 10
- 롱노트: 15

Main Normal:
- 타이밍 이벤트: 209
- 실제 레인 노트: 226
- 동시입력: 17
- 롱노트: 20

Main Hard:
- 타이밍 이벤트: 365
- 실제 레인 노트: 424
- 동시입력: 59
- 롱노트: 17

## 확인 포인트

- 브라우저 정책상 곡 미리듣기와 게임 오디오는 사용자가 곡 또는 Start를 누른 뒤 재생됩니다.
- 미리듣기 중 `Start`를 누르면 미리듣기는 멈추고, 카운트다운 이후 실제 플레이용 오디오가 처음부터 시작됩니다.
- 성능 확인은 Fever 구간, 롱노트 hold 구간, Hard 하이라이트 구간을 우선으로 보면 좋습니다.
