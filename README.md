# 이라크 아침 뉴스 · NIC 동향 자동 웹 대시보드

> 준비 파일은 기존 2026년 11월 18~24일 ChatGPT 브리핑을 보관하고 있으며, 이후 **공개 RSS에서 발견한 뉴스 제목**을 매일 수집하는 GitHub Pages용 웹사이트입니다. 중요한 보도는 반드시 원문을 확인하세요.

## 빠른 설정 (브라우저만 사용)

1. https://github.com/signup 에서 **GitHub 무료 계정** 생성.
2. https://github.com/new 에서 새 저장소 `iraq-news` 생성. **Public** 선택, **Add README 선택하지 않기**.
3. 다운로드한 ZIP의 압축을 풀고, 그 **안의 모든 파일·폴더**를 선택합니다 (`.github`, `data`, `public`, `update.py`, `template.html`, `README.md`, `requirements.txt` 등). 최상위 폴더를 통째로 넣어 하위 폴더가 하나 더 생기지 않게 주의합니다.
4. 빈 저장소 화면의 **uploading an existing file** 또는 **Add file → Upload files**를 누르고 파일·폴더를 끌어다 놓은 다음 **Commit changes**를 클릭합니다. 최상위에 `update.py`, `template.html` 등이 있어야 합니다.
5. 저장소 **Settings → Pages → Build and deployment → Source: GitHub Actions** 선택.
6. 저장소 **Actions** 탭 → **이라크 뉴스 자동 업데이트 및 웹 배포** → **Run workflow** → 초록색 성공 여부를 확인.
7. 웹사이트 열기: `https://YOUR_GITHUB_USERNAME.github.io/iraq-news/` (YOUR_GITHUB_USERNAME은 본인의 계정명으로 변경). Settings → Pages에도 접속 주소가 표시됩니다.

## AI 한국어 요약 사용 (선택 사항)

이 단계가 없어도 **공개 RSS 기사 제목의 원어 표시 + 날짜별 기록 + 페이지 자동 배포**는 가능합니다. 다만 제목을 한국어로 자동 번역·요약하려면 OpenAI API를 따로 설정해야 합니다.

1. https://platform.openai.com/api-keys 에서 API 키 생성. API 사용료는 ChatGPT 구독과 **별도**입니다.
2. GitHub 저장소 **Settings → Secrets and variables → Actions → New repository secret**.
3. 이름을 `OPENAI_API_KEY`, 값에 API 키를 입력하고 저장. **API 키를 코드, README, 채팅, 공개 파일에 넣지 마세요.**
4. **Actions → Run workflow**로 실행해 한국어 요약이 추가되는지 확인.
5. 기본 모델은 `gpt-6.1-terra`입니다. 변경하려면 Settings → Secrets and variables → Actions → Variables의 `OPENAI_MODEL`에 지원되는 모델 ID를 설정할 수 있습니다.

## 자동화 일정

- GitHub Actions: 매일 **UTC 04:10 = 바그다드 오전 07:10** 예약.
- GitHub 예약 워크플로는 실행이 지연되거나 드물게 생략될 수 있습니다. 07:00 정각 업데이트를 보장하지 않습니다.
- 자동으로 `data/news.json`과 `public/index.html`을 갱신·저장하고 Pages에 재배포합니다.
- 별도 서버가 필요 없으며 공개 저장소에서 GitHub Pages·일반 Actions 실행을 무료로 이용할 수 있습니다. 서비스 조건과 한도는 GitHub 정책에 따릅니다.
- 스스로 실행해 보고 싶을 때 **Actions → Run workflow**를 사용합니다.

## 뉴스 수집 방식과 한계 — 꼭 확인

- 일반 뉴스: Google News 공개 RSS에서 검색한 제목과 게시일을 수집합니다. 원문 전체를 자동 분석·검증하지 않으므로, 구체적 금액·실제 지급 여부는 원문과 대조해야 합니다.
- NIC: 공식 웹사이트 공개 RSS가 접근 가능하고 출처가 확인되는 경우에만 `NIC 공식 RSS`로 표기합니다. 검색 결과의 NIC 관련 기사는 **공식 발표로 확정하지 않습니다.** 공식 홈페이지의 모든 변경 이력을 추적할 수는 없습니다.
- Facebook 지정 페이지: 접근 제한 때문에 **원 게시물·수정 내역 자동 확인 기능이 없습니다.** 상태 항목으로 제한을 알려줍니다. FB가 업데이트되지 않았다고 단정하지 않습니다.
- Bismayah / Hanwha: RSS에 발견된 관련 기사만 자동 표시합니다. **계약변경합의서 승인, 미수금 지급, 실제 입금, 소유권 증서 발행** 등 공식 확정 여부는 수동 검증이 필요합니다.
- AI 키가 없는 경우 신규 제목은 아랍어/영어 등 원어로 표시됩니다. 키가 있는 경우에도 입력 범위는 RSS 제목·게시일·출처이므로 ChatGPT에서 수동 조사한 일일 브리핑과 정확히 같지 않습니다.
- 과거 11월 18~24일 기록은 기존 채팅에 등장한 브리핑 요약의 보관본이며 별도 재검증된 데이터가 아닙니다.
- **Public 저장소와 Pages 웹사이트는 누구나 볼 수 있습니다.** 비공개 업무 정보나 회사 내부자료를 업로드하지 마세요.

## 오류 확인

- **웹사이트 404**: Settings → Pages가 `GitHub Actions`로 되어 있는지, Actions의 마지막 실행이 성공했는지 확인합니다.
- **업데이트 안 됨**: Actions → 워크플로 → 최근 실행 내역을 열고 `Collect RSS news and build site`, `Publish website` 로그를 확인합니다. RSS 접근 오류면 자동 수집될 기사 수가 0개일 수 있습니다.
- **에러: Resource not accessible by integration / 403**: 저장소 Settings → Actions → General → Workflow permissions에서 Actions의 권한을 검토합니다. 보안 정책 때문에 쓰기가 제한될 수 있습니다.
- **AI 요약이 안 됨**: `OPENAI_API_KEY` 이름, OpenAI API 잔액·청구 설정, 워크플로 로그를 확인합니다. 오류 시 원어 제목으로 자동 전환합니다.
- **파일 경로 확인**: `.github/workflows/daily.yml`에 자동화 파일이 있어야 합니다. `.github` 폴더를 누락하면 자동 실행되지 않습니다.

### 파일 구성

```text
iraq-news/
├── .github/workflows/daily.yml   # 자동 실행·배포
├── data/news.json                # 날짜별 브리핑 데이터
├── public/index.html             # 웹사이트 (자동 생성)
├── public/.nojekyll
├── template.html                 # 웹페이지 원형
├── update.py                     # 수집·요약·기록·웹페이지 생성
├── requirements.txt
└── README.md
```

기술 참고: [GitHub Pages](https://docs.github.com/en/pages), [GitHub Actions 예약 실행](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows), [OpenAI API](https://developers.openai.com/api/docs/quickstart).
