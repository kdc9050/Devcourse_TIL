#git 강의

- git이 필요한 이유??

  - 버전 관리 시스템
    - 수정 사항 기록, 누가, 언제, 무엇을, 왜 ?: 커밋 메시지를 통해 의도를 드러내기
    - 특정 시점으로 고정
    - 수정 내역을 추적
    - 이전 상태로 되돌림
  - 일상 속 버전 관리
    - 노션
    - 구글 드라이브
  - 도구들
    - gitkraken(유료)
    - sourcetree(무료)

- git 설정

  - git config --global user.name "사용자 이름"
  - git config --global user.email "사용자 이메일"
  - git config --global --list
  - git config --global --edit

- git 명령어에도 적용되는 파레토 법칙

  - 20%의 명령어로 80%의 작업을 처리할 수 있다.
  - git add, git commit, git push
  - git status, git log, git checkout, git branch
  - git reset, git revert, git rebase, git merge
  - git clone, git pull, git fetch

- git 저장소 생성

  - git init [<directory>]
  - git status
  - git add <file>
  - git commit -m "메시지"

- Commit..
  - 의미 있는 변화..
    - 커밋은 언제 해야 할까..? => e.g) React 프로젝트 생성, 회원 인증 기능 추가, 버튼 클릭 버그 수정, 리렌더링 최적화
- branch, checkout

  - 작업의 분기점
    - 브랜치는 언제 만들어야 할까..? => e.g) 새로운 작업을 시작하기 전, issue가 나에게 할당된 후, 이 시점을 백업해두고 싶을때, 새로운 버전을 출시하기 전
  - git branch <branch-name>
  - git checkout(switch/restore) : 브랜치 이동
  - git checkout <branch-name>

- merge

  - 나뉘어진 분기의 통합
  - git merge <branch-name>
  - 충돌이 발생할 수 있다.
  - 충돌을 해결하고 merge commit을 생성한다.

- conflict

  - 발생 이유
    - 협업자 간 Git History가 일치하지 않는 경우
  - 대처 방법
    - 충돌 파악 후 틀어진 History를 봉합
      - 충돌 위치(파일과 라인))
      - 충돌 유형(코드 스타일 차이, 동시 추가, 리팩터링)
      - 충돌 원인(어떤 커밋, 이력이 틀어진 시점)
  - 충돌이 발생했을 때 하면 안 되는 것
    - 두 사람 이상이 관여된 conflict를 혼자서 해결하기 (단순 코드 스타일 ,의존성 lock 파일 제외)
    - Hash에 영향을 주는 작업 후 git push --force 명령어 치기 (`rm -rf /`과 같음)

- git vs github
  - git
    - 분산 버전 관리 시스템
    - 로컬 저장소
  - github
    - git을 호스팅하는 서비스
    - 원격 저장소
- git push --force
  - 강제로 push
  - 절대로 사용하면 안되는 이유 : 다른 사람의 작업을 덮어쓰기 때문에
- rebase
  - 커밋 이력을 깔끔하게 정리
  - git rebase <base-branch>
