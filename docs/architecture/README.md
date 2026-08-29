# 아키텍처 다이어그램

## homerun-build.architecture.html

빌드·실행 토폴로지. 로컬 개발부터 CI/CD, 컨테이너 실행까지 한 장에 있다.
**브라우저로 그냥 열면 된다.** 단독 HTML이라 서버도 의존성도 필요 없다.

- 노드의 `SRC` 배지 → 그 노드가 실제로 어느 파일에서 온 건지 열어 준다
- 상단 Guided views → 로컬 실행 / 테스트 / 커밋에서 이미지까지, 경로별로 재생
- Export → PNG, SVG, 공유 카드

뷰어 UI(Light/Dark, Present, Export)는 영어로 나온다. 생성 도구가 한국어 로케일을
지원하지 않아서다. 다이어그램 내용 자체는 한국어다.

## 고칠 때

`.html` 을 직접 손대지 않는다. 원본은 `homerun-build.architecture.json` 이다.
JSON 을 고치고 다시 렌더링한다:

```bash
npx skills add tt-a1i/archify --agent claude-code --skill '*' --yes

node ~/.claude/skills/archify/bin/archify.mjs deliver architecture \
  docs/architecture/homerun-build.architecture.json \
  docs/architecture/homerun-build.architecture.html \
  --quality showcase --repo-root .
```

`deliver` 는 검증에 실패하면 파일을 쓰지 않는다. 통과하면 뷰포트 확인까지 한다:

```bash
node ~/.claude/skills/archify/bin/archify.mjs visual-check \
  docs/architecture/homerun-build.architecture.html
```

`meta.repository.revision` 에 커밋 SHA 가 박혀 있다. 파일 경로가 바뀌면 `sources` 도
같이 고쳐야 검증을 통과한다.
