# Git

## git init

git init 명령어로 local에 git repository를 생성할 수 있다.

```bash
git init
```

## git add

git add 명령어로 unstaged 파일들을 staging area에 추가할 수 있다.
추가하고 싶은 파일 이름을 add 뒤에 입력하면 된다.

```bash
git add <path>
```

모든 파일을 추가하고 싶은 경우 add 뒤에 \*를 사용하면 된다.

```bash
git add *
```

## git restore

git restore 명령어를 통해 unstaged 파일의 변경사항을 최신 커밋으로 되돌릴 수 있다.

```bash
git restore <path>
```

이미 staging 파일인 경우 --staged 옵션을 이용해 staging area에서 제거할 수 있다. --staged 옵션은 변경사항은 되돌리지 않으므로 필요한 경우 옵션 없이 restore를 한번 더 수행해줘야 한다.

```bash
git restore --staged <path>
```

## git commit

git commit 명령어를 통해 현재 staging area에 있는 파일 변경사항들을 커밋할 수 있다. unix shell에서 커밋을 실행하면 커밋 메세지를 작성할 수 있는 에디터에 진입한다.

```bash
git commit
```

-m 옵션을 통해 에디터에 진입하지 않고 바로 커밋 메세지를 작성할 수 있다.

```bash
git commit -m "commit message"
```

--amend 옵션을 통해 최신 커밋을 수정 가능하다. -m 옵션과 함께 이용하면 커밋 메세지도 수정이 가능하다.
<br>
_\* 실제로는 최신 커밋을 직접 수정하는 게 아니고 최신 커밋을 제거하고 최신 커밋 변경사항 + 현재 변경사항으로 새로운 커밋을 생성하는 방식이므로 주의해야 한다._

```bash
git commit --amend -m "new commit message"
```

## git log

git log 명령어를 통해 현재 브랜치의 커밋 로그를 조회할 수 있다.
옵션을 통해 다양한 방식으로 출력 가능하다.

- patch : 변경된 파일의 변경 내용까지 출력한다
- stat : 변경된 파일들과 변경된 라인 수 정보를 출력한다
- oneline : 요약된 커밋 해시코드 및 메세지를 출력한다
- graph : 브랜치 커밋 히스토리를 그래프 형태로 보여준다.

<br>

```bash
git log [--patch] [--stat] [--oneline] [--graph]
```

<br>

# Git Branch

## HEAD

현재 git에서 가리키고 있는 커밋 노드를 나타낸다. git에서 수행하는 동작은 HEAD의 커밋이 기준이 된다. 커밋을 수행하면 HEAD 다음에 커밋이 생성되고, HEAD가 새로 생성된 커밋으로 변경된다.

## Branch

브랜치는 git에서 변경사항의 분기를 편하기 관리하게 해주는 커밋의 포인터 역할을 한다. 브랜치를 변경하면 브랜치가 가리키는 커밋으로 HEAD가 변경된다.

## git branch

git branch 명령어를 통해 현재 저장소의 브랜치 목록을 조회할 수 있다. branch만 입력할 경우 브랜치 이름만 출력된다.

- a 옵션을 추가하면 원격 저장소의 브랜치 목록도 조회 가능하다
- v 옵션을 추가하면 각 브랜치의 HEAD 커밋에 대한 정보도 함께 출력한다

```bash
git branch [-a] [-v]
```

## git checkout

git checkout 명령어를 통해 브랜치를 변경할 수 있다.
