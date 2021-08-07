# Git branch

## 1. Branch 관련 명령어

> 사전 root commit 있어야 함

1. Branch 생성

    ```bash
    (master) $ git branch (branch_name)
    ```

2. Branch 이동

    ```bash
    (master) $ git checkout (branch_name) #구버전
    (master) $ git switch (branch_name) #신버전
    ```

3. Branch 생성 및 이동

    ```bash
    (master) $ git checkout -b (branch_name)
    ```

4. Branch 삭제

    ```bash
    (master) $ git branch -d (branch_name)
    ```

5. Branch 목록

    ```bash
    (master) $ git branch
    ```

6. Branch 병합

    ```bash
    (master) $ git merge (branch_name)
    ```

	* master 브랜치에서 (branch_name)을 병합



## 2. Branch 병합 시나리오

### 	S1. fast-foward 

> fast-foward는 feature 브랜치 생성된 이후 master 브랜치에 변경 사항이 없는 상황

1. feature/about branch 생성 및 이동

   ```bash
   (master) $ git checkout -b feature/about
   (feature/about)
   ```

2. 작업 완료(about.html 파일 생성) 후 commit

   ```bash
   $ touch about.html
   $ git status
   $ git add .
   $ git commit -m 'Complete About page'
   ```

3. log 결과 확인

   ```bash
   $ git log
   ```


3. master 이동

   ```bash
   (feature/about) $ git checkout master
   (master)
   ```


4. master에 병합 > fast-foward (단순히 HEAD를 이동)

  ```bash
  $ git merge feature/about
  ```

5. 결과 확인(log) 

   ```bash
   $ git log
   ```

6. branch 삭제

   > 병합이 완료된 브랜치는 삭제!
   
   ```bash
   $ git branch -d feature/about
   ```

---

### 	S2. merge commit

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 **다른 파일이 수정**되어 있는 상황
>
> git이 auto merging을 진행하고, **commit이 발생된다.**

1. feature/main branch 생성 및 이동

   ```bash
    $ git checkout -b feature/main
   ```

2. 작업 완료 후 commit

   ```bash
   $ touch main.html
   $ git status
   $ git add .
   $ git commit -m 'Complete main.html'
   ```

3. log 확인

   ```bash
   $ git log
   ```

4. master 이동

   ```bash
   $ git switch master
   ```

5. *master에 추가 commit 이 발생시키기!!*

   * **다른 파일을 수정 혹은 생성**

   ```bash
   $ touch other.html
   $ git add .
   $ git status
   $ git commit -m 'Complete other.html'
   ```

6. master에 병합 -> 자동으로 *merge commit 발생*

   ```bash
   $ git merge master
   ```

7. 결과 (log 확인)

   ```bash
   $ git log
   commit 0243d6244abc9c845f284424a575eb79d66640b8 (HEAD -> master)
   Merge: b1d93a2 bdc9a20
   Author: mellunk <jjyju1344@gmail.com>
   Date:   Thu Aug 5 13:56:52 2021 +0900
   
       Merge branch 'feature/main'
   
   commit b1d93a2428279349507bb245c8f84f56d60e1066
   Author: mellunk <jjyju1344@gmail.com>
   Date:   Thu Aug 5 13:49:47 2021 +0900
   
       Complete other.html
   
   commit bdc9a20ee19d5971a9be00df0939454cd1dcf01d (feature/main)
   Author: mellunk <jjyju1344@gmail.com>
   Date:   Thu Aug 5 13:48:04 2021 +0900
   
       Complete main.html
   
   ```

8. 그래프 확인하기

   ```bash
   $ git log --oneline --graph
   ```

9. branch 삭제

   ```bash
   $ git branch -d feature/main
   ```

---

### 	S3. merge commit 충돌 

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 **같은 파일의 동일한 부분이 수정**되어 있는 상황
>
> git이 auto merging을 하지 못하고, 충돌 메시지가 뜬다.
>
> 해당 파일에 직접 들어가서 수정후 커밋 하기



1. feature/board branch 생성 및 이동

   ```bash
   $ git branch feature/board
   ```

2. 작업 완료(board.html) 후 commit (log 확인)

   ```bash
   $ touch board.html
   $ git status
   $ git add .
   $ git commit -m 'Complete board.html'
   ```



3. master 이동

   ```bash
   $ git switch master
   ```
   


4. *master에 추가 commit 이 발생시키기!!*

   ```bash
   $ git commit -m 'Update Readme.md again'
   ```

5. master에 병합

   ```bash
   git merge master
   ```
   


6. 결과 -> *merge conflict발생*

   > git status 명령어로 충돌 파일을 확인할 수 있음.
   
   ```bash
   $ git merge master
   Auto-merging README.md
   CONFLICT (content): Merge conflict in README.md
   Automatic merge failed; fix conflicts and then commit the result.
   ```
   


7. 충돌 확인 및 해결

   ```bash
   직접 해당파일 열어서 수정하기
   타이포라는 안예쁘니까 vs나 메모장 열어서 수정
   $ git add .
   ```
   


8. merge commit 진행

   ```bash
   $ git commit -m 'Fix conflict'
   ```

   * vs code 창 닫기

9. 그래프 확인하기

    ```bash
    $ git log --oneline --graph
    *   f6fbc01 (HEAD -> feature/board) Fix conflict
    |\
    | * de73503 (master) Update README.md
    | * 74977db Complete board.html
    * | 43fddfd Update Readme.md again
    |/
    *   0243d62 Merge branch 'feature/main'
    |\
    | * bdc9a20 Complete main.html
    * | b1d93a2 Complete other.html
    |/
    * 3834617 Complete About page
    * 5877bb1 add text
    * 11991ed branchpractice
    ```


10. branch 삭제

    ```bash
    $ git branch -d feature/board
    ```
    
    ***
    
    
    
    ### 상황1. 
    
    + 브랜치에서 커밋
    + master에서 커밋할 때 어떤 커밋도 없었음
    
    ### 상황2.
    
    + 브랜치에서 커밋
    + master에서 병합할 때 어떠한 커밋이 있음
      + 다른 파일이 수정된 상황
    
    ### 상황3
    
    + 브랜치에서 커밋
    + master에서 병합할 때 어떠한 커밋이 있는데, 이게 같은 파일이 수정된 것.
      + 파일을 열어서 충돌난 부분을 확인하여 고치고(내맘대로)
      + add .
    + 직접 merge commit

***

## 끝말잇기 실습

##  A

최초에 한번 클론

```bash
$ git clone [url주소]
```

---

제시어  -> README.md에 작성

```bash
$ git add .
$ git commit -m '~'
$ git push origin master
```

B에 'pull 받아주세요.'

## B

```bash
$ git pull origin master
```

README.md에 작성

반복!

***

## 왜 Staging area가 필요한가?

+ **여러 파일들을** 작업하는 과정에서 어떠한 파일을 버전으로 기록할 지 모아두는 곳

+ 파일 하나만 작업할 땐 그 유용성을 모를 수 있으나 여러 파일을 동시에 작업할 떄 필수 불가결

***

## Pull Request

