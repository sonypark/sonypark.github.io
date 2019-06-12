2019년 4월 4일

# 코드스쿼드 Git PR 과정

---

### 1. 저장소 브랜치에 자신의 github 아이디에 해당하는 브랜치가 있는지 확인한다. 
    
    - 브랜치가 없는 경우 마스터에게 브랜치 생성을 요청한다.

### 2. 프로젝트를 자신의 계정으로 fork한다.

### 3. fork한 프로젝트를 자신의 컴퓨터로 clone한 후 디렉토리로 이동한다.

```bash
git clone -b {본인_아이디} --single-branch https://github.com/{본인_아이디}/{저장소 아이디}
ex) git clone -b sonypark --single-branch https://github.com/sonypark/java-racingcar
cd {저장소 아이디}
ex) cd java-racingcar
```

### 4. 기능 구현을 위한 브랜치 생성

```bash
git checkout -b 브랜치이름
ex) git checkout -b step1
```

### 5. 기능 구현 후 `add`, `commit`

### 6. 본인 원격 저장소에 올리기

```bash
git push origin 브랜치이름
ex) git push origin step1 # 원격저장소(origin)에 step1 브랜치를 올린다.
```

### 7. github 서비스에서 pull request 를 보낸다.

> pull request는 original 저장소의 브랜치(자신의 github 아이디)와 앞 단계에서 생성한 브랜치 이름을 기준으로 한다. 
> 
> pull request를 통해 피드백을 받으면 코드를 수정한 후 같은 브랜치에 add, commit, push 작업을 반복한다.

### 8. 리뷰어(마스터)는 피드백을 마무리하고 codesquad 저장소로 merge한다.

### 9. merge를 완료했다는 통보를 받으면 브랜치 변경 및 작업 브랜치 삭제(option)한다.
 
 ```bash
 git checkout 본인_아이디
 git branch -D 삭제할_브랜치이름
 ex) git checkout sonypark
 ex) git branch -D step1
```

### 10. merge한 codesquad 저장소와 동기화하기 위해 codesquad 저장소 추가한다.(최초 한번만)

- 동기화를 하는 이유는 로컬 저장소 브랜치와 원격 저장소 브랜치의 버전이 다르기 때문이다.
- 이전에 로컬 저장소(sonypark 브랜치)에서는 step1 브랜치를 만들어 작업하고 push 하고 삭제했다.
- 따라서 로컬의 sonypark 브랜치에는 step1 브랜치에서 작업한 내용이 없는 상태이다.

```bash    
git remote add {저장소_별칭} base_저장소_url
ex) git remote add upstream https://github.com/code-squad/java-racingcar.git

// 위와 같이 codesquad 저장소를 추가한 후 전체 remote 저장소 목록을 본다.
git remote -v
```

### 11. codesquad 저장소에서 자기 브랜치 가져오기(또는 갱신하기)

```bash    
git fetch upstream {본인_아이디}
ex) git fetch upstream sonypark
```

### 12. codesquad 저장소 브랜치와 동기화하기

```bash
git rebase upstream/본인_아이디
ex) git rebase upstream/sonypark
```

### 13. 4단계부터 다시 진행