# skill_MCP

Codex에서 사용할 MCP 구성을 한곳에서 관리하기 위한 워크스페이스입니다.

## 권장 구성

| 기능 | 권장 방식 | 이유 |
|---|---|---|
| Context7 | MCP | 최신 라이브러리/프레임워크 문서 조회 |
| Playwright | MCP | 브라우저 자동화/웹 테스트 |
| GitHub | MCP | Issue/PR/원격 저장소 작업 |
| Docker MCP Toolkit | MCP Gateway | Docker Desktop에서 MCP 서버를 프로필로 관리 |
| Filesystem | Codex 기본 도구 우선 | Codex가 로컬 파일/셸을 직접 다룰 수 있어 중복 MCP를 피함 |
| Git | Codex 기본 `git` CLI 우선 | 별도 Git MCP 없이도 대부분의 작업 가능 |

> 원칙: MCP는 필요한 것만 켭니다. 도구를 많이 등록하면 시작 컨텍스트와 도구 선택이 복잡해질 수 있습니다.

## 디렉터리

```text
skill_MCP/
├─ configs/
│  ├─ wsl.config.example.toml
│  ├─ windows.config.example.toml
│  └─ homeserver.config.example.toml
├─ docs/
│  └─ SETUP.md
└─ .gitignore
```

## 추천 사용 구조

- **WSL Codex**: 메인 개발 환경. Context7 + Playwright + GitHub + Docker Toolkit.
- **Windows Codex**: Windows 전용 파일/GUI 작업이 필요할 때만.
- **Home Server Codex**: 서버 운영용. Context7/GitHub 정도만 두고 최소 구성 권장.

## 보안

실제 `~/.codex/config.toml`, Personal Access Token, API Key, OAuth 캐시 등은 이 저장소에 올리지 않습니다.
이 저장소에는 예제 설정만 보관합니다.

자세한 적용 방법은 [docs/SETUP.md](docs/SETUP.md)를 참고하세요.
