### TIL(2019-04-04) Git, Git Stash

---

#### 이동

- 일했다정기석 채널에서 음악을 들으니 버질 아블로가 생각났고 편집의 시대임을 실감했다.

- Javascript 강의를 듣지 않았다는 이야기다. 전 날 2시까지 다 못 한 미션을 했더니 피곤해서 도저히 들을 수가 없었다. 들을 수가 없었다기 보다는 그러고 싶지 않았다. 역시 체력의 총량은 보존되나보다.



#### 코드스쿼드

> ##### 오전 / 오후

- 오전과 오후 거의 내내 호눅스의 GIt 강의를 들었고 강의 후에는 팀 별로  팀 Repository에 Pull Request를 보내 merge하고 다시 내 Repository에 fetch, rebase하는 것까지 해보았다. 



- A라는 branch에서 파일을 만들고 B라는 branch에서 add를 한 뒤 A branch에서 commit을 하니 A branch로 commit되는 현상을 발견했다. 

  Working Directory에서 tracked되지 않은 파일은 branch와 상관 없이 있는 것이고 stage는 branch마다 있는 게 아니라 branch가 다 공유하고 있음을 알게 되었다. 

  때문에 2개 이상의 branch로 작업을 할 때 commit을 하지 않은 채 branch를 변경해 작업을 해야 하는 경우에는 stash를 사용해서 하던 일을 넣어두고 branch를 변경해 작업을 해야 한다고 한다. 

  Stash는 Working Directory에 Modified이면서 tracked 상태인 파일과 Staging Area에 있는 파일들을 보관해두는 장소다. 잠깐 SAVE하는 개념인듯 하다. 

```

git stash

// 이름을 부여해서 저장할 수 있다. 현재 작업을 저장하고 branch를 head로 돌린다.
git stash push

// save와 push가 같은 역할을 하나 push 사용이 추천됨
git stash save [이름]

// stash로 저장된 목록을 확인
git stash list

// 마지막으로 저장된 stash 불러오기, stash list에서는 사라진다
git stash pop

// 특정 stash를 불러올 수 있다. 
git stash apply stash@{0}

// 필요없는 stash 삭제
git stash drop

// stash 전체 삭제
git stash clear
```

직접 파일을 만들어서 stash를 해보니 A Branch에서 stash를 한 것을 B branch에서도 사용할 수 있었다.



- 알고리즘 2문제를 풀어봤지만 답을 맞추진 못했다. 백준에서 풀어봤는데 프로그래머스에서 주로 알고리즘을 풀다보니 백준에서 값을 입력 받고 디버깅을 하는 것에 익숙하지가 않아 문제를 풀면서 자주 버벅거린다.



- 감기 기운에 일찍 들어가 숙면함

---

#### 요약

- GIt 공부 (stash를 알게 됨)
- 알고리즘 2문제 (오답)

