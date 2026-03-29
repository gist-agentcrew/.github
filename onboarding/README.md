# GEAR 온보딩 가이드

GEAR(GIST Educational Agentic Researchers)에 오신 것을 환영합니다!

## 우리는 누구인가

GEAR는 광주과학기술원(GIST) 소속 AI Agent 연구·교육 팀입니다.
각자의 관심 도메인에서 문제를 정의하고, AI Agent를 활용하여 문제를 해결하는 과정에서 Agent를 연구합니다.

> ***"Build your own Agent. Own your data."***

## 우리의 원칙

| 원칙 | 의미 |
|------|------|
| No External API (in production) | 최종 산출물은 외부 API에 의존하지 않는다 |
| Local First | 로컬/자체 서버에서 동작한다 |
| Open Source | 모든 산출물을 공개한다 |
| Anyone Can Build | 누구나 만들 수 있도록 설계한다 |

> 개발 과정에서는 외부 API와 AI 도구를 자유롭게 사용해도 됩니다.
> 단, 최종 산출물은 로컬에서 동작해야 합니다.

## 스터디 운영 방식

### 전체 흐름

```
1. 관심 도메인 선정 → 문제 정의
2. Agent 프레임워크 선택 (Agent, PyAgent, OpenClaw, Harness 등)
3. 디스코드 채널에서 연구 진행
4. 매주 금요일 12:30 정기세션에서 발표
5. GitHub Organization 블로그에 마크다운으로 정리
```

### 디스코드 사용법

서버 구조:
```
📁 공지·운영
   ├── #공지사항        ← 주간 공지, 일정 안내
   ├── #일정            ← 발표 일정, 스프린트
   └── #온보딩          ← 이 가이드가 핀 고정되어 있음

📁 공용
   ├── #자유토론        ← 자유롭게 대화
   ├── #질문답변        ← 궁금한 것 질문
   ├── #자료공유        ← 논문, 링크, 참고자료
   └── #발표            ← 발표 자료 공유

📁 본인 이름 (예: pjm38)
   └── #연구노트        ← 기본 채널 (자유롭게 채널 추가 가능)
```

- **본인 카테고리** 안에서 자유롭게 채널을 만들 수 있습니다.
- 채널명은 연구 주제에 맞게 바꿔도 됩니다.
- 다른 팀원의 채널도 열람 가능합니다 (서로 배우기 위해).

### 블로그

- 연구 결과는 GitHub Organization 블로그에 마크다운으로 정리합니다.
- 정제된 언어로 작성해주세요 (다른 사람이 읽을 수 있도록).

## 환경 세팅

### 필수
- Python 3.10 이상
- Git 설치 및 기본 사용법 숙지
- Discord 계정 + GEAR 서버 참여

### 인프라

```
┌──────────────────────┐
│  DGX Spark 2대       │  ← 큰 모델 서빙 (vLLM, Qwen3)
│  (분산 컴퓨팅)        │
└──────────┬───────────┘
           │ 내부 네트워크
┌──────────▼───────────┐
│  Mobile X (엣지)      │  ← 소형 모델 (7B~8B 양자화)
│  RTX 3000            │
└──────────────────────┘
```

## 디스코드 봇 연동 방법

각자의 채널에 AI Agent를 디스코드 봇으로 연동할 수 있습니다.

### Step 1: 봇 만들기
1. https://discord.com/developers/applications 접속
2. **New Application** → 이름 입력 → **Create**
3. 왼쪽 메뉴 **Bot** → **Reset Token** → 토큰 복사 (안전하게 보관)
4. **Privileged Gateway Intents** 설정:
   - **Presence Intent**: 멤버의 온라인/오프라인 상태 읽기
   - **Server Members Intent**: 멤버 목록 조회, 입장/퇴장 이벤트 수신
   - **Message Content Intent**: 채팅 메시지 내용 읽기 (명령어 인식에 필수)

### Step 2: 봇 서버 초대
1. 왼쪽 메뉴 **OAuth2** → **OAuth2 URL Generator**
2. Scopes: `bot` 체크
3. Bot Permissions: 필요한 권한 체크 (Send Messages, Read Message History 등)
4. 생성된 URL로 GEAR 서버에 초대

### Step 3: 봇 코드 작성 (Python 예시)
```python
import discord
from discord.ext import commands

bot = commands.Bot(command_prefix="!", intents=discord.Intents.default())

@bot.event
async def on_ready():
    print(f"봇 로그인: {bot.user}")

@bot.command()
async def hello(ctx):
    await ctx.send("안녕하세요! GEAR 봇입니다.")

bot.run("YOUR_BOT_TOKEN")  # .env에서 불러오세요!
```

### 주의사항
- 봇 토큰은 절대 GitHub에 올리지 마세요.
- `.env` 파일에 저장하고, `.gitignore`에 `.env`가 포함되어 있는지 확인하세요.
- 봇은 스크립트를 실행하는 동안만 동작합니다. 24시간 운영하려면 서버에서 계속 실행해야 합니다.

## 질문이 있다면

- 디스코드 #질문답변 채널에 질문해주세요.
- 팀장: 박주민 (@pjm38)
