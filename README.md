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

### staged 옵션

이미 staging 파일인 경우 --staged 옵션을 이용해 staging area에서 제거할 수 있다. --staged 옵션은 변경사항은 되돌리지 않으므로 필요한 경우 옵션 없이 restore를 한번 더 수행해줘야 한다.

```bash
git restore --staged <path>
```

## git clean

git clean 명령어를 통해 staging area에 추가되지 않은 모든 tracked 파일 변경사항을 되돌릴 수 있다.

> _\* tracked : 현재 HEAD 커밋 히스토리에서 커밋된 적 있는 파일들. git에서 변경사항을 추적하고 있는 파일들을 말한다._

```bash
git clean
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

### amend 옵션

amend 옵션을 통해 최신 커밋을 수정 가능하다. -m 옵션과 함께 이용하면 커밋 메세지도 수정이 가능하다.

> _실제로는 최신 커밋을 직접 수정하는 게 아니고 최신 커밋을 제거하고 새로운 커밋을 생성하는 방식이므로 주의해야 한다. 이미 공유된 커밋을 수정할 경우 해당 커밋을 기반으로 작업하던 작업자들과 충돌이 생길 수 있다._

```bash
git commit --amend [-m "new commit message"]
```

### fixup 옵션

fixup 옵션을 사용하면 커밋을 생성하고, 현재 커밋이 특정 커밋과 함께 적용됐어야 할 변경사항임을 표현해줄 수 있다. 즉, 예전에 한 커밋에 변경사항을 추가하고 싶을 때 사용한다.
커밋할 때 실제로 예전 커밋을 변경하는 것은 아니다. 추후에 rebase를 수행할 때 이 옵션을 사용한 커밋을 분석해서 변경사항 적용 순서를 바꿔서 적용한다.

```bash
git commit --fixup <target_commit>
```

> _fixup을 사용하면 특수한 커밋이 생성되는 것이 아니라, 커밋 메세지 앞에 fixup!이라는 문자열이 추가된다. 이를 git에서 특정 동작을 수행할 때 명령어로 해석해서 작업을 수행할 때 반영한다._

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

-d 옵션을 이용하면 브랜치를 제거할 수 있다.

```bash
git branch -d <branch>
```

## git checkout

git checkout 명령어를 통해 브랜치를 변경할 수 있다.

```bash
git checkout <branch>
```

-b 옵션을 이용하면 새로운 브랜치를 생성하고 생성한 브랜치로 변경한다.

```bash
git checkout -b <new_branch>
```

## git switch

git switch 명령어를 통해서도 브랜치를 변경할 수 있다. git에서 브랜치는 변경하는 최신 문법이다. 동작은 git checkout과 유사하다.

```bash
git switch <branch>
```

-c 옵션을 이용하면 새로운 브랜치를 생성하고 생성한 브랜치로 변경한다.

```bash
git switch -c <new_branch>
```

# Merge 동작

Git에서는 branch끼리 달라진 변경사항을 다시 하나로 병합할 수 있다.
머지에는 두 가지 종류가 있다.
병합을 시도하는 브랜치를 source, 병합의 대상이 되는 브랜치를 target이라고 할 때 source와 target이 분기되는 base 커밋에 따라 머지 방식이 달라진다.

1. **Fast foward**

   base에서 source 브랜치가 변경되지 않은(커밋을 수행하지 않은) 경우이다. source가 가리키는 커밋을 target의 최신 커밋으로 변경만 하면 된다.

2. **3-way merge**

   두 브랜치 모두 base 이후에 커밋을 따로 수행한 경우에는 두 브랜치가 가리키는 커밋을 각각 참조하여 새로운 커밋을 만들어서 브랜치가 기리키는 커밋을 변경한다.

> _양쪽 브랜치에서 같은 파일에서 동일한 라인을 수정했다면, 깃은 머지 과정에서 충돌이 발생했다고 판정하게 된다._
>
> _git은 충돌이 발생하면 해당 파일에 대해 충돌이 발생했다고 마킹하고 사용자가 직접 해당 파일의 충돌을 해결하도록 수정을 요구한다._
>
> _충돌 판정을 받은 파일을 사용자가 다시 git add로 staging 영역에 추가하면, git은 다시 충돌을 판정하지 않고 이전 파일 내용을 해당 파일로 변경하는 것을 확정한다. 기존과 완전히 다른 내용으로 파일을 재작성해도 git은 신경쓰지 않고 머지 커밋을 수행한다._

## git merge

git merge 명령어를 통해 다른 브랜치의 변경사항을 현재 브랜치에 반영할 수 있다. 변경사항을 가져오고 싶은 브랜치(target)를 merge 명령어 뒤에 작성한다.

```bash
git merge <target>
```

git merge를 수행하면 Fast foward 머지 상황의 경우 바로 머지가 수행되고, 3-way 머지가 필요한 경우 새로운 커밋 작성을 수행한다.
3-way 머지를 수행하면 두 브랜치 변경사항이 합쳐진 새로운 커밋이 생성되고, 현재 브랜치는 해당 커밋을 가리키게 된다. 이 때 커밋 로그에서는 양쪽 브랜치의 커밋 내역이 시간 순서대로 합쳐서 출력된다.

## git rebase

git rebase 명령어를 통해서도 다른 브랜치의 변경사항을 현재 브랜치에 반영할 수 있다.

```bash
git rebase <target>
```

merge 명령어와 다른 점은 target 브랜치와 커밋 히스토리를 공유하지 않고, merge 커밋을 따로 생성하지 않는다는 점이다.
source에서 base로부터 생성된 커밋 변경사항을 target의 최신 커밋부터 순차적으로 반영하는 커밋 히스토리를 새로 생성한다.

### interactive 옵션

git rebase 명령어에 -i 옵션을 추가하면 rebase 실행 시 수행될 커밋 적용 과정을 에디터를 통해 직접 편집할 수 있다.

```bash
git rebase -i <target>
```

실행하면 에디터에 pick, squash 등 git에서 정의한 rebase 전용 DSL을 이용한 todo 리스트를 보여준다.

```bash
pick <commit_hash> <commit message>
```

### rebase -i 주요 명령어

- pick : 대상 커밋을 그대로 적용.
- reward : 대상 커밋의 메세지만 수정하고 pick.
- edit : 대상 커밋까지 정의한 동작을 수행한 상태에서 직접 git 명령 수행. rebase 재개 시 동작은 edit 종료 후에 HEAD 기준으로 진행됨.
- squash : 이전 커밋과 대상 커밋 변경사항을 합친 새로운 커밋을 생성해서 적용. 커밋 메세지를 별도로 작성해야 함.
- fixup : 이전 커밋과 대상 커밋 변경사항을 합친 새로운 커밋을 생성해서 적용. 대상 커밋 메세지는 무시하고 앞 커밋 메세지 사용.

이 옵션을 이용해서 불필요한 커밋을 제거하거나, 커밋 메세지를 수정하는 등 복잡한 커밋 히스토리를 깔끔하게 정리할 수 있는 다양한 작업을 수행할 수 있다.

### git merge / rebase 동작 표현

---

<br>

```python
# 기존 git commit history
A(base) -> A+B(source)
 \
   -> A+C1 -> A+C2(target)

# (source) git merge target
A(base) -> A+B -------------> D(source)
 \                        /
   -> A+C1 -> A+C2(target)

# (source) git rebase target
# source에서 변경한 커밋 변경사항들을 target 커밋에서부터 차례로 적용
A(base) -> A+B(source:before)
 \
   -> A+C1 -> A+C1+C2(target) -> A+C1+C2+B(source)
```

### git merge vs git rebase

두 방식의 커밋 히스토리는 다르고 최종적으로 완성되는 브랜치의 결과물은 동일하다.

merge 명령어의 경우 히스토리가 합쳐진 흔적이 남고, 히스토리 또한 시간 순대로 혼재되어 있어 변경 내역을 제대로 추적하기 어렵다. 하지만 모든 변경 과정이 그대로 남기 때문에 변경 기록이 중요한 경우에는 merge를 사용하는 것이 좋다.

rebase 명령어의 경우 머지된 흔적이 없이 처음부터 하나의 브랜치에서 작업한 것처럼 보여지므로 커밋 히스토리가 깔끔해지고 변경사항을 추적하기 쉽다. 하지만 원본 수정 내역을 확인하기 어렵고, 새로운 커밋을 생성하는 방식이기 때문에 다른 작성자와 공유 중인 커밋에 대해 rebase를 수행하면 위험할 수 있다.

_\* 보통 로컬에서 개인 작업할 때, PR을 보내기 전에 커밋 내역을 정리할 때 rebase를 사용하고, 공식 브랜치에서 머지를 수행하거나 같이 공유 중인 브랜치를 수정할 때에는 머지를 사용하면 좋다._

# 커밋 내역 수정

## git revert

git revert를 이용하면 특정 버전의 커밋으로 파일을 되돌리는 새로운 커밋을 생성할 수 있다.

```bash
git revert <target_commit>
```

## git reset

git reset을 이용하면 현재 HEAD를 특정 버전의 커밋으로 되돌릴 수 있다.

> _\* 기존에 작성한 커밋 내역이 바로 사라지지는 않으므로 git reflog 명령어를 통해 유실된 커밋 내역을 조회할 수 있다._

### mixed 옵션

git reset에 아무 옵션도 주지 않았을 때 적용되는 기본 옵션이다. 특정 버전의 커밋으로 되돌리면서 staging area의 상태도 해당 커밋 기준으로 초기화된다.

```bash
git reset [--mixed] <target_commit>
```

### soft 옵션

soft 옵션을 이용하면 mixed 옵션과 유사하게 동작하지만, staging area는 변하지 않는다. staging area에 있던 파일들이 soft reset 후에 git status로 조회해도 그대로 남아 있는 것을 볼 수 있다.

```bash
git reset --soft <target_commit>
```

### hard 옵션

hard 옵션을 적용하면 HEAD를 특정 버전의 커밋으로 되돌리면서, 동시에 변경한 파일들도 해당 커밋의 상태로 초기화할 수 있다. 기존 작업 내용이 모두 사라질 수 있으므로 사용에 주의해야 한다.

_\* 단, 돌아간 커밋 시점에서 아직 추적되고 있지 않았던 파일들은 삭제되거나 초기화되지 않는다. 예를 들어 커밋 이후 새로 생성해서 작성한 파일들은 hard 옵션을 이용해서 reset해도 변경되지 않고 그대로 남아 있는다._

```bash
git reset --hard <target_commit>
```

## git cherry-pick

cherry-pick 명령어를 통해 현재 HEAD부터 적용하고 싶은 커밋만 선택해서 적용할 수 있다. 브랜치의 작업을 깔끔하게 정리하고 싶을 때 사용하면 좋다.

```bash
# HEAD에서 commit1부터 차례대로 적용
git cherry-pick <commit1> <commit2> ...
```

## git stash

stash 명령어를 사용하면 현재 작업 중인 변경사항을 임시로 저장하고 최신 커밋으로 파일들을 되돌릴 수 있다.

현재 작업 중인 내역을 커밋하기 전에 다른 브랜치로 변경해야 하거나, 현재 작업하던 내역들을 새로운 브랜치로 분리하고 싶을 때 사용하면 편리하다.

별도로 stash 이름을 지정해주지 않으면 가장 최근에 저장한 stash 기준으로 동작을 수행한다.

### 작업 내역 저장

```bash
git stash
```

### 작업 내역 적용

```bash
git stash apply
```

### 작업 내역 적용 및 제거

```bash
git stash pop
```

### 작업 내역 삭제

```bash
git stash drop
```
