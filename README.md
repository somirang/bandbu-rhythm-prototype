# 4Key Rhythm Prototype

밴드부 리듬게임 노트 제작 참고용 standalone HTML 프로토타입입니다. 노트 타이밍, 밀도, 난이도 곡선, 동시입력, 롱노트, 피버, 입력감을 빠르게 확인하는 용도입니다.

## 실행 방법

1. `index.html`을 브라우저에서 엽니다.
2. 시작 화면에서 `Tutorial`, `ClassRoom`, `Recruitment`, `Main` 중 하나를 고릅니다.
3. `Main`을 고른 경우 `Easy`, `Normal`, `Hard` 중 하나를 고릅니다. `Tutorial`, `ClassRoom`, `Recruitment`는 난이도 선택 없이 바로 시작합니다.
4. 화면 중앙의 `Start`를 누른 뒤 `D / F / J / K`로 플레이합니다.
5. 곡이 끝나면 결과창에서 점수, 최대 콤보, 정확도, 판정 수, Stage Sync, Story Impact, 랭크를 확인하고 `Replay`로 다시 시작할 수 있습니다.

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

- 4키 고정: `D / F / J / K`
- 곡 선택: `Tutorial / ClassRoom / Recruitment / Main`
- Main 난이도: `Easy / Normal / Hard`
- Tutorial은 단일 쉬운 차트로 구성
- ClassRoom은 튜토리얼 다음 단계용 단일 차트로 구성
- Recruitment는 영입 신경전 장면용 단일 차트로 구성
- 오른쪽에서 왼쪽으로 접근하는 노트
- 인게임 HUD: Combo, Score, Accuracy, Fever, Stage Sync, Perfect/Great/Good/Miss 카운트
- 결과창: Final Score, Max Combo, Accuracy, Stage Sync, Story Impact, 판정 수, Rank, Replay
- 입력 tick, 성공 hit, 실패 miss, Fever start 사운드
- 롱노트 hold 중 노트/레인/판정선 glow, pulse, trail 피드백
- Fever Time 중 배경/판정선 pulse, 화면 가장자리 glow, 약한 흔들림
- Canvas 기반 stage light, hit burst, particle, judgement pop/fade

## 차트 방향

- Tutorial은 약 93 BPM 기준으로 다시 분석한 박자 위상에 맞춰 배치했고, 메인 Easy보다 훨씬 쉽게 설계했습니다.
- Tutorial은 처음 4초 동안 노트가 없고, 이후 `단노트 -> 롱노트 -> 2키 동시입력 -> 종합 복습` 순서로 학습합니다.
- Tutorial의 1/4 구간은 단노트만, 2/4 구간은 롱노트만, 3/4 구간은 2키 동시입력만 사용합니다.
- ClassRoom은 약 103 BPM 기준으로 다시 분석한 정박 위상에 맞춰 배치했고, 마지막 3초 이상은 노트가 나오지 않도록 피날레를 정리했습니다.
- ClassRoom은 처음 4초 동안 노트가 없고, `준비 도입 -> 교실 그루브 -> 빌드업 -> 하이라이트 -> 회복 -> 피날레` 구조로 밀도가 오르내립니다.
- Recruitment는 약 136 BPM 기준으로 다시 분석한 정박 위상에 맞춰 배치했고, ClassRoom과 비슷하거나 아주 약간 더 긴장감 있게 설계했습니다.
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
