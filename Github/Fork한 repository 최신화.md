# Fork한 repository 최신화

Fork한 repository를 최신화 시켜야 할 때 가 있다.  
이를 위해 원본 repository를 remote repository로 추가해야한다.  
아래 명령어를 입력하면 다음과 같이 출력된다.

```
$ git remote -v
```

여기에 동기화 하고싶은 repository를 upstream이라는 이름으로 추가한다.

```
$ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
```

upstream이 제대로 추가되었는지 확인한다.

```
$ git remote -v
```

이제 upstream repository로 부터 최신 업데이트를 가져온다.

```
$ git fetch upstream
```

upstream repository 의 master branch (혹은 원하는 branch) 로부터 나의 local master branch 로 merge 한다.

```
$ git checkout master
$ git merge upstream/master
```

이제 로컬 repository에 push 해준다

```
git push origin master
```
