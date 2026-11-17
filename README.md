# welKome 부스 화면 (변경 파일만)

[SeungYunChoi0/welKome-ai-agent](https://github.com/SeungYunChoi0/welKome-ai-agent)의 `demo/live-pipeline` 가지(커밋 `6f0691e`)에서 **바뀐 파일과 새 파일만** 모은 저장소입니다. 2026 CO-SHOW 부스 화면용입니다.

- 부스 벽에 맞춘 새 스킨(오른쪽 검색 패널과 바탕). 휴대폰 화면 모양은 그대로입니다.
- 아래 탭: 홈 · **시연** · 챗봇(맛집 탭은 화면에서만 뺌).
- 시연 탭: 저장해 둔 질문 10개의 기록을 휴대폰과 검색 패널에 반복 재생. 60초 동안 아무도 만지지 않으면 시연 탭으로 넘어갑니다.
- 글꼴 내장(인터넷 없이도 같은 화면).

자세한 내용은 [docs/BOOTH_DEMO.md](docs/BOOTH_DEMO.md)에 있습니다.

## 적용 방법

서버 자산(`app/assets/`)과 `app/.env`가 있는 컴퓨터에서:

```bash
git clone -b demo/live-pipeline https://github.com/SeungYunChoi0/welKome-ai-agent.git
git clone https://github.com/dawnnam02/welKome-booth-screen.git
cp -r welKome-booth-screen/frontend welKome-booth-screen/tools welKome-booth-screen/docs welKome-ai-agent/
cd welKome-ai-agent
bash run_demo.sh                 # http://127.0.0.1:8001
```

기존 작업 폴더가 있으면 마지막 `cp` 줄만 그 폴더로 하면 됩니다. 서버 코드(`app/`)는 바꾸지 않았습니다.

## 실제 시연 기록 만들기

`frontend/static/demo_runs.json`은 처음엔 **예시 데이터**입니다(휴대폰 아래에 「· 예시」 표시). 서버를 켠 상태에서 한 번 실행합니다.

```bash
python tools/record_demo.py      # 질문 10개, 생성 모델 유료 호출 20회 안팎, 5~10분
```

## 파일

| 파일 | 원래 저장소 대비 |
|---|---|
| `frontend/index.html` | 바꿈: 새 스킨 구조, 맛집 탭 → 시연 탭, 시연 화면 추가 |
| `frontend/static/style.css` | 바꿈: 앞부분(휴대폰)은 원래 그대로, 뒷부분이 새 스킨과 시연 화면 |
| `frontend/static/script.js` | 바꿈: 한 줄(직접 질문 전에 시연 재생을 끝냄) |
| `frontend/static/demo.js` | 새 파일: 시연 재생기 |
| `frontend/static/demo_runs.json` | 새 파일: 시연 기록(예시) |
| `frontend/static/fonts/` | 새 파일: Noto Sans KR · Noto Serif KR · Jua(한글·라틴만 남김) |
| `frontend/static/images/13_ink_band.png` | 새 파일: 아래쪽 산수화 띠 |
| `tools/record_demo.py` | 새 파일: 실제 시연 기록 저장 |
| `docs/BOOTH_DEMO.md` | 새 파일: 안내 |

## 라이선스

원래 저장소와 같은 MIT License(`LICENSE`). 글꼴은 SIL Open Font License 1.1(`frontend/static/fonts/OFL-*.txt`).
