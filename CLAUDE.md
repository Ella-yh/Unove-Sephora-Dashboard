# Unove Sephora Dashboard — 작업 규칙

## 커밋 메시지 규칙 (필수)

Claude는 코드 수정을 완료할 때마다 **푸시용 커밋 메시지를 반드시 제안**한다.
사용자(윤희)는 GitHub Desktop에서 해당 메시지로 커밋 → Push origin.

형식: `<타입>: <한국어 요약 (50자 내외)>`

| 타입 | 용도 | 예시 |
|------|------|------|
| `feat` | 기능 추가 | `feat: 광고 차트 CTR 지표 추가` |
| `fix` | 버그 수정 | `fix: 월 필터 라벨 5월 이후 빈 표시 수정` |
| `perf` | 성능 개선 | `perf: 캐시 SWR 적용 + 인증/데이터 페치 병렬화` |
| `refactor` | 동작 동일, 구조 개선 | `refactor: 광고 지표 상태 차트별 분리` |
| `style` | UI/디자인만 변경 | `style: KPI 카드 여백 조정` |
| `docs` | 문서 | `docs: 작업 규칙 추가` |
| `chore` | 설정·기타 | `chore: 디버그 콘솔 로그 제거` |

## 작업 워크플로

1. Claude가 클론 폴더의 `index.html` 직접 수정
2. 수정 후: JS 문법 검증(node --check) + diff 요약 보고 + **커밋 메시지 제안**
3. 윤희: GitHub Desktop에서 diff 확인 → 커밋 → Push origin
4. GitHub Pages 자동 배포 (~1분) → Ctrl+Shift+R로 확인

## 프로젝트 구조 메모

- 단일 파일 SPA: `index.html` (GitHub Pages 호스팅: ella-yh.github.io/Unove-Sephora-Dashboard)
- 데이터: Google Apps Script(`pivot_전체raw` 등 시트 파싱) → JSON, 클라이언트는 localStorage 캐시(SWR) 사용
- 인증: Google OAuth implicit flow, @wyattcorp.com 도메인 제한
- 주의: 줄바꿈이 CRLF — 전체 줄 변경처럼 보이는 diff는 줄바꿈 노이즈. 실제 diff는 `git diff --ignore-cr-at-eol`로 확인
- Apps Script 수정 시 "배포 관리 → 수정 → 새 버전" 필수 (저장만으로는 미반영)
