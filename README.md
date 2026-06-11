# Band Note Lab 4Key Normal

밴드부 리듬게임 노트 제작 참고용 standalone HTML 프로토타입입니다. 최종 게임이 아니라 노트 타이밍, 밀도, 난이도 곡선, 동시입력, 롱노트, 피버, 입력감을 빠르게 확인하는 용도입니다.

## 실행 방법

1. `index.html`을 브라우저에서 엽니다.
2. 화면 중앙의 `Start`를 누릅니다.
3. `Easy` 또는 `Normal`을 고른 뒤 `D / F / J / K`로 플레이합니다.
4. 곡이 끝나면 결과창에서 점수, 콤보, 정확도, 판정 수를 확인하고 `Replay`로 다시 시작할 수 있습니다.

파일 직접 열기가 막히는 브라우저에서는 이 폴더에서 로컬 서버를 실행해 확인하세요.

```powershell
& "C:\Users\HS\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe" -m http.server 4173
```

그다음 브라우저에서 `http://localhost:4173`을 엽니다.

## 포함 파일

- `index.html`: standalone 실행 파일입니다. 차트가 HTML 안에도 내장되어 있어 단독 실행 가능합니다.
- `main.wav`: 플레이에 사용하는 오디오입니다.
- `chart_main_4key_easy.json`: 4키 Easy 차트 원본입니다.
- `chart_main_4key_normal.json`: 4키 Normal 차트 원본입니다.
- `note_chart_easy_4key.csv`: Easy 스프레드시트 검토용 노트 목록입니다.
- `note_chart_normal_4key.csv`: Normal 스프레드시트 검토용 노트 목록입니다.
- `assets/ui`: 현재 프로토타입 UI/노트 참고 에셋입니다.
- `assets/design`: 첨부 디자인 분위기 참고용 에셋입니다.

## 판정 기준

- Perfect: +/-40ms
- Great: +/-80ms
- Good: +/-145ms
- Miss: Good 범위 밖 또는 노트가 지나간 경우

## 현재 기능

- 4키 고정: `D / F / J / K`
- 난이도: `Easy / Normal`
- 오른쪽에서 왼쪽으로 접근하는 노트
- 인게임 HUD: Combo, Score, Accuracy, Perfect/Great/Good/Miss 카운트
- 중앙 난이도 선택 Start 오버레이와 곡 종료 Result 오버레이
- Replay 시 곡, 노트, 점수, 콤보, 판정 카운트 전체 초기화
- 짧은 입력 tick, 성공 hit, miss/빈 입력 약한 피드백
- 롱노트 hold 중 노트, 레인, 판정선 glow/pulse 피드백
- Canvas 기반 hit burst, particle, judgement pop/fade
- 피버 게이지와 하이라이트 구간 약한 판정선 pulse

## 차트 방향

- BPM 100 기준으로 2~4마디 단위 반복/변형 루프를 사용했습니다.
- 주요 루프는 `D F J K`, `K J F D`, `D F -> J K`, `D+J`, `F+K`입니다.
- 잔잔한 구간은 넓은 간격의 단일 노트, 빌드업은 8분음표 중심, 하이라이트는 밀도 증가와 2키 동시입력을 사용합니다.
- `D+K`, `F+J`는 하이라이트 구간에서만 제한적으로 사용했습니다.
- JSON/CSV에는 `section`, `pattern`, `intent`가 포함되어 노트 제작 의도를 확인할 수 있습니다.

## 현재 통계

Easy:

- 타이밍 오브젝트: 163개
- 실제 레인 노트: 173개
- 동시입력: 10개
- 롱노트: 15개

Normal:

- 타이밍 오브젝트: 209개
- 실제 레인 노트: 226개
- 동시입력: 17개
- 롱노트: 20개
- 패턴 정의: 27개
