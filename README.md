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

## git clean

git clean 명령어를 통해 staging area에 추가되지 않은 모든 tracked 파일 변경사항을 되돌릴 수 있다.

_\* tracked : 현재 HEAD 커밋 히스토리에서 커밋된 적 있는 파일들. git에서 변경사항을 추적하고 있는 파일들을 말한다._

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

--amend 옵션을 통해 최신 커밋을 수정 가능하다. -m 옵션과 함께 이용하면 커밋 메세지도 수정이 가능하다.
<br>
_\* 실제로는 최신 커밋을 직접 수정하는 게 아니고 최신 커밋을 제거하고 새로운 커밋을 생성하는 방식이므로 주의해야 한다. 이미 공유된 커밋을 수정할 경우 해당 커밋을 기반으로 작업하던 작업자들과 충돌이 생길 수 있다._

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
target에서 base로부터 생성된 커밋 변경사항을 source 브랜치 최신 커밋부터 순차적으로 반영하는 커밋을 새로 생성한다.

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

보통 로컬에서 개인 작업할 때, PR을 보내기 전에 커밋 내역을 정리할 때 rebase를 사용하고, 공식 브랜치에서 머지를 수행하거나 같이 공유 중인 브랜치를 수정할 때에는 머지를 사용하면 좋다.

# 변경사항 되돌리기

## git reset

git reset을 이용해 현재
