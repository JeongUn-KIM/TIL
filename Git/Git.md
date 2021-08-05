# 버전관리?

+ 정의 : 동일한 정보에 대한 여러 버전을 관리하는 것

버전관리 소프트 웨어 종류 다양

오늘, Git 에 대해 학습

*****

## Git 기초흐름

1. **Git이란?** 분산버전관리 시스템

- 컴퓨터 파일의 변경사항 추적 및 여러 사용자 간에 해당 파일 작업을 조율



2. **분산버전관리시스템(DVCS)** 

   - *원격 저장소*를 통해 여러 작업자들이 협업하고 모든 히스토리를 클라이언트들이 공유
   - 나누어진 버전을 합치는 것도 합리적

   

3. 기본 흐름

   + **작업**  --  **add**하여 *Staging area*에 모아 -- **commit**으로 버전 기록
   + Git은 파일을 modified, staged

   

4. Git 영역 구성

   + **Working Directory** (Local)

     : 개인 코드 작성

   + **Staging 영역**

     : git add를 통해 수정된 코드를 올림

   + **Repository**

     : git commit을 통해 최종 수정본을 제출

     

5. 파일 라이프사이클

<img src="C:\Users\jjyju\AppData\Roaming\Typora\typora-user-images\image-20210804160742388.png" alt="라이프사이클" style="zoom: 50%;" />

+ Working directory의 모든 파일은 특정 상태를 가지며, git 명령어를 통해 변경함
  + Tracked : 이전부터 버전으로 관리되고 있는 파일
    + Unmodified : git status에 나타나지 않음
    + Modified : Changes not staged for commit
    + Staged : Changes to be committed
  + Untracked : 버전으로 관리된 적 없는 파일 (새로만든 파일)

****

## 기초 CLI 명령어

> CLI(Command Line Inteface) 
>
> - git 열면 나오는 검정화면
> - 인터페이스 구성 : 명령 - 결과
>
> GUI 환경인 윈도우와는 다른 인터페이스를 지닌다

+ ls : 목록 (= list )

  ```bash
  $ ls
  1.txt
  ```

+ **touch** : 파일 만들기

  ``` bash
  $ touch <파일명>
  $ touch README.md
  ```

+ pwd : 현재 작업 디렉토리 출력 (= print working directory)

  ```bash
  $ pwd
  /c/Users/jjyju/OneDrive/바탕 화면/멀티캠퍼스/특강/Git,Github/실습1
  ```

+ mkdir = 디렉토리  만들기 (=make directory)

  ```bash
  $ mkdir test
  ```

+ cd test : 디렉토리 이동 (= change directory test)

  ```bash
  ~/Desktop/실습1/test $ cd test
  $ cd ..
  ```
  
  + . . : 상위 디렉토리
  +   . : 현재 디렉토리햣 

***

+ **git init** : git 저장소를 만듬

  ```bash
  $ git init
  Initialized empty Git repository in C:/Users/jjyju/OneDrive/바탕 화면/멀티캠퍼스/특강/Git,Github/실습1/.git/
  ```

+ **git add** : working directory 상의 변경내용을 staging area에 추가

  > untracked, modified 상태 --> staged

  ```bash
  $ git add 파일.확장자
  $ git add a.txt
  ```

+ **git commit** : staged 상태의 파일들을 commit을 통해 버전으로 기록함

  ```bash
  $ git commit -m '커밋메세지'
  $ git commit -m 'a.txt'
  [master (root-commit) 04c1918] a.txt
   1 file changed, 0 insertions(+), 0 deletions(-)
   create mode 100644 a.txt
  ```

+ **git status** : git 저장소에 있는 파일의 상태 확인

  ```bash
  $ git status
  현재 상태 출력
  ex)
  No commits yet
  ex)
  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
          new file:   a.txt
  ex)
  nothing to commit, working tree clean
  
  ```

+ **git log** : 현재 저장소에 기록된 커밋을 조회

  ```bash
  $ git log -1
  $ git log -oneline
  $ git log -2 --oneline
  
  commit 7c0845f128bff2b8506cd3aa5be3365fd915bb4f (HEAD -> master, origin/master)
  Author: mellunk <jjyju1344@gmail.com>
  Date:   Wed Aug 4 15:46:25 2021 +0900
  
      Add R
      EADME.md
  ```
  

***

## Git 설정파일(config)

- 사용자 정보(author) : 커밋을 하기위해 반드시 필요함

  - git config --global user.name *" username"*
  - git config --global user.email *"my@email.com"*

  -> 둘 다 깃헙에서 설정한 username, email 사용

- 설정 내용 확인 방법

  - git config -l
  - git config --global -l
  - git config user.name



## 원격저장소 활용 명령어

+ clone : 원격저장소를 복제하여 가져옴

  > **클론(clone)**으로 가져온 것은 과거 모든 이력을 받아옴
>
  > 압축 풀어서 가져온 것은 과거 이력 x .git x  => 활용 어려움

  ```bash
  $ git clone <원격저장소 주소>
  ```


+ **push** : 원격저장소로 로컬저장소 변경사항(commit)을 올림(push) 

  ```bash
  $ git push <원격저장소 이름> <브랜치 이름>
  $ git push origin master
  
  Enumerating objects: 4, done.
  Counting objects: 100% (4/4), done.
  Delta compression using up to 12 threads
  Compressing objects: 100% (3/3), done.
  Writing objects: 100% (3/3), 1.17 KiB | 1.17 MiB/s, done.
  Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
  To https://github.com/mellunk/TIL.git
     7c0845f..e2cc8b4  master -> master
  ```

+ pull : 원격저장소로 부터 변경된 내역 받아와서 이력을 병합함

  ```bash
  $ git pull <원격저장소 이름> <브랜치 이름>
  ```

+ git remote add origin

+ git remote rm origin

+ git push origin master
