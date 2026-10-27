## 워크 플로우
1. 이슈를 GitHub Issue에 먼저 등록한다. IssueConvention.md 참조.
2. 등록한 이슈에 맞는 branch를 main-develop에서 개설한다. BranchConvention.md 참조.
3. 개설한 브랜치에서 작업을 진행한다. FileCompositionConvention.md, BasicCodeConvention.md, AntiCodeConvention.md, RecommandedCodeConvention.md 참조.
4. 작은 단위(새 스크립트 작성 혹은 수정)가 끝나면 커밋을 진행한다. CommitConvention.md 참조.
5. 하나의 기능 구현(혹은 문서 작성, 기능 수정)이 완료가 되었을 때, Pull Request를 진행한다. PullRequestConvention.md 참조.
6. Pull Request가 완료되어 Merge까지 충돌없이 완료되면 관련 이슈를 Close 한다. 
7. 이슈가 Close 되면 개설한 브랜치를 Delete 한다.