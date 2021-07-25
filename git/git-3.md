# git3
실제로 일어날 수 있는 상황.

## 충돌
git push를 할 때, remote repo의 내용이 업데이트 되어있는 상황이라면 push가 되지 않는다. 이 때, pull을 먼저 해야하는데, 만약 작업한 부분이 같다면 pull 명령이 update된 내용을 가져와서 merge 하는 명령이기 때문에 conflict가 발생한다.

conflict가 발생한 파일을 수정해서 다시 add, commit, push를 진행하면 된다.

## 원격 레포에 잘못된 코드가 올라가 있을 때
git pull은 업데이트된 코드를 가져와서 merge 한다고 했었다. 그러나 바로 머지하고 싶지 않을 수도 있다. 확인 후 원할 때 머지 할 수 있도록 업데이트 되어있는 코드를 가져오기만 하는 명령이 바로 fetch. 
```
git fetch
git diff premium origin/premium
```
fetch를 한 뒤 diff 명령으로 로컬의 premium branch와 remote의 premium branch를 비교할 수 있다.

만약 여기서 remote에 잘못된 내용이 들어가 있다면 두 가지 방법으로 이를 수정할 수 있다.
1. 해당 커밋 개발자에게 직접 얘기해서 remote에 업데이트 해달라고 요청
2. 직접 잘못된 부분을 해결을 하고 push하기

2번의 경우 merge를 해서 잘못된 코드를 수정하고 다시 커밋을 한다. 

## 한가지 파일의 이력을 보아야 할 때.
```
git blame <파일>
...
git show <COMMIT_HASH>
```
blame은 비난하다, 탓하다 라는 뜻을 가진다. 코드의 잘못된 부분이 있을 때 해당 코드를 작성한 개발자에게 책임을 묻는다는 의미로 볼 수 있는데, 그만큼 커밋에 대한 책임을 부여하고 프로젝트 관리를 수월하게 할 수 있도록 한다.

## 이미 원격 레포에 올라간 코드를 취소해야 할 때
```
git revert <COMMIT_HASH>
```
해당 커밋을 삭제하고 그 내용을 커밋하는 것 까지 자동으로 해주는 명령. 만약 특정 범위에 있는 커밋을 모두 되돌리고 싶다면 다음과 같이 범위를 써주면 된다.
```
# ab12 커밋 "다음" 부터 cd34 커밋까지 모두 삭제한다고 가정
git revert ab12..cd34
```
ab12를 제외하고, 그 다음 커밋부터 모두 revert 한다