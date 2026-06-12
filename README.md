# 4Key Rhythm Prototype

밴드부 리듬게임 노트 제작 참고용 standalone HTML 프로토타입입니다. 최종 게임이 아니라 노트 타이밍, 밀도, 난이도 곡선, 동시입력, 롱노트, 피버, 입력감을 빠르게 확인하는 용도입니다.

## 실행 방법

1. `index.html`을 브라우저에서 엽니다.
2. 시작 화면에서 `Easy`, `Normal`, `Hard` 중 하나를 고릅니다.
3. 화면 중앙의 `Start`를 누른 뒤 `D / F / J / K`로 플레이합니다.
4. 곡이 끝나면 결과창에서 점수, 최대 콤보, 정확도, 판정 수, Stage Sync, Story Impact, 랭크를 확인하고 `Replay`로 다시 시작할 수 있습니다.

파일 직접 열기가 막히면 이 폴더에서 로컬 서버로 확인하세요.

```powershell
& "C:\Users\HS\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe" -m http.server 4173
```

그다음 브라우저에서 `http://localhost:4173`을 엽니다.

## 포함 파일

- `index.html`: standalone 실행 파일이며 Easy/Normal/Hard 차트가 내장되어 있습니다.
- `main.wav`: 플레이 음악입니다.
- `chart_main_4key_easy.json`: Easy 차트 원본입니다.
- `chart_main_4key_normal.json`: Normal 차트 원본입니다.
- `chart_main_4key_hard.json`: Hard 차트 원본입니다.
- `note_chart_easy_4key.csv`: Easy 노트 제작 검토용 CSV입니다.
- `note_chart_normal_4key.csv`: Normal 노트 제작 검토용 CSV입니다.
- `note_chart_hard_4key.csv`: Hard 노트 제작 검토용 CSV입니다.
- `assets/ui`: 현재 UI와 노트 참고 에셋입니다.

## 판정 기준

- Perfect: +/-60ms
- Great: +/-110ms
- Good: +/-180ms
- Miss: Good 범위 밖, 노트를 놓친 경우, 롱노트를 너무 일찍 놓친 경우

## 현재 기능

- 4키 고정: `D / F / J / K`
- 난이도: `Easy / Normal / Hard`
- 오른쪽에서 왼쪽으로 접근하는 노트
- 인게임 HUD: Combo, Score, Accuracy, Fever, Stage Sync, Perfect/Great/Good/Miss 카운트
- 결과창: Final Score, Max Combo, Accuracy, Stage Sync, Story Impact, 판정 수, Rank, Replay
- 키 입력 tick, 성공 hit, 실패 miss, Fever start 사운드
- 롱노트 hold 중 노트/레인/판정선 glow, pulse, trail 피드백
- Fever Time 중 배경/판정선 pulse, 화면 가장자리 glow, 약한 흔들림
- Canvas 기반 stage light, hit burst, particle, judgement pop/fade

## 차트 방향

- BPM 100 기준 2~4마디 단위 반복/변형 루프를 사용합니다.
- 주요 루프는 `D F J K`, `K J F D`, `D F -> J K`, `D+J`, `F+K`, `D+K`, `F+J`입니다.
- Easy는 넓은 간격과 쉬운 단일 노트 중심입니다.
- Normal은 빌드업과 하이라이트에서 밀도, 롱노트, 2키 동시입력이 늘어납니다.
- Hard는 공연형 riff, 손 교대, 2키 코드, 짧은 16분 느낌 pickup을 더 많이 사용합니다.
- JSON/CSV에는 `section`, `pattern`, `intent`가 포함되어 노트 제작 의도를 확인할 수 있습니다.

## 현재 통계

Easy:
- 타이밍 이벤트: 163
- 실제 레인 노트: 173
- 동시입력: 10
- 롱노트: 15

Normal:
- 타이밍 이벤트: 209
- 실제 레인 노트: 226
- 동시입력: 17
- 롱노트: 20

Hard:
- 타이밍 이벤트: 365
- 실제 레인 노트: 424
- 동시입력: 59
- 롱노트: 17
