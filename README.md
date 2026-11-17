# welKome 부스 화면 (변경 파일만)

[SeungYunChoi0/welKome-ai-agent](https://github.com/SeungYunChoi0/welKome-ai-agent)의 `demo/live-pipeline` 가지(커밋 `6f0691e`)에서 **바뀐 파일과 새 파일만** 모은 저장소입니다. 2026 CO-SHOW 부스 화면용입니다.

- 부스 벽에 맞춘 새 스킨(오른쪽 검색 패널과 바탕). 휴대폰 화면은 원래 디자인 그대로, 크기만 1.2배.
- 아래 탭: 홈 · **시연** · 챗봇(맛집 탭은 화면에서만 뺌).
- **홈**: 장소 사진 5곳(경복궁, 종묘, 흥인지문, 돈화문, 사직단)을 ◀ ▶ 버튼이나 손으로 밀어 고르면 아래에 장소 소개와 실록 이야기가 나옵니다.
- **시연**: 실제 서버로 기록해 둔 질문 5개를 휴대폰과 검색 패널에 반복 재생. 60초 동안 아무도 만지지 않으면 시연 탭으로 넘어갑니다.
- 글꼴 내장(인터넷 없이도 같은 화면). 홈과 시연은 저장된 기록으로 돌아가므로 서버를 부르지 않습니다. 챗봇 탭의 직접 질문만 실제 서버로 갑니다.

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

기존 작업 폴더가 있으면 마지막 `cp` 줄만 그 폴더로 하면 됩니다. 서버 코드(`app/`)는 바꾸지 않았습니다. 브라우저는 새로 고침(Ctrl+F5)으로 열어 주세요.

## 들어 있는 기록

| 파일 | 내용 | 확인 |
|---|---|---|
| `frontend/static/demo_runs.json` | 시연 질문 5개(실록 속 고양이, 암행어사 권한, 사도세자 가정, 6·25 전쟁, 호랑이 출현)의 실제 답변과 검색 과정 | 답변의 연도·기사를 조선왕조실록 사이트와 대조함. 부스 안내판의 다른 질문 5개는 답변에 틀린 곳이 있어 뺌 |
| `frontend/static/places.json` | 장소 5곳의 사진 인식 결과, 장소 소개, 실록 이야기 | 실록 이야기의 연도·사건을 대조함. 틀린 곳이 있던 경복궁·사직단은 다시 받음 |

다시 기록하려면 서버를 켠 뒤 `python tools/record_demo.py`, `python tools/record_places.py --url <서버 주소>` (유료 호출이 생깁니다).

## 출처와 라이선스

- 코드: 원래 저장소와 같은 MIT License(`LICENSE`).
- 글꼴: Noto Sans KR, Noto Serif KR, Jua — SIL Open Font License 1.1(`frontend/static/fonts/OFL-*.txt`).
- 장소 사진: 위키미디어 공용, 작가와 라이선스(CC BY / CC BY-SA)는 `frontend/static/images/places/CREDITS.md`와 화면 속 사진 아래에 표시.
- 기록 파일 속 실록 문장: 『조선왕조실록』 국역본 © 한국고전번역원(원문 제공: 국사편찬위원회 조선왕조실록 사이트). 시연을 위한 인용이며 위 라이선스의 대상이 아닙니다. 권리자가 요청하면 해당 부분을 지우겠습니다.
- 답변과 실록 이야기는 AI(실록이)가 만든 글입니다.
