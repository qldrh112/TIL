# 2024.01.12

## CLI를 통한 GIT 사용과 GITHUB

### 기본적인 CLI 명령

|**명령어**|**설명**|
|:------:|:---:|
|mkdir|폴더 생성|
|tough|파일생성|
|ls|현재폴더의 목록출력|
|cd|다른 폴더로 이동|
|rm|파일삭제/폴더 삭제(-r옵션)|
|..|상위 디렉터리|
|.|현재 디렉터리|
|/|디렉터리 사이의 구분자|
|start|파일 열기|
|exit|터미널 종료|
|clear|터미널 정리|
|`tab`|자동 완성|
|`↕`|이전에 사용한 명령 불러오기|


### 기본적인 GIT 명령
|**명령어**|**설명**|
|:------:|:---:|
|git init|.git 파일 생성|
|git add|스테이징 서버에 추가|
|git commit (-m '메시지')|저장소에 추가|
|git status|파일의 상태 확인|
|git log (--oneline)|파일의 commit 이력 확인|
|git commit --amend|commit된 git log 수정|
|git remote -v|등록된 원격 저장소 확인|
|git add remote '별명' 'URL'|로컬과 원격저장소 연결|
|git push '별명' 'branch'|commit 내용을 원격저장소에 반영|
|git pull '별명' 'branch'|원격 저장소에서 변경 사항을 로컬에 반영|
|git clone URL|URL의 원격 저장소를 복제하여 로컬에 저장|
|clear|터미널 정리|
|`tab`|자동 완성|
|`↕`|이전에 사용한 명령 불러오기|

#### .gitignore ####
협업을 하며 상대방과 운영체제, 사용 프로그램, 버전까지 다를 때가 존재할 것이다. 문제는 비전 관리를 할 때 충돌이 발생하면 상당히 머리가 아픈데 그 때, 발생할 수 있는 충돌을 방지하기 위해서 .gitignore 파일을 만들고 파일명을 리스트업 한다. 그렇게 되면, git의 관리에서 해당 파일을 제외된다. 

관련해서 도움이 되는 웹사이트를 공유받았다.

[자신의 프로젝트에 꼭 맞는 .gitignore 파일을 만드세요](https://www.toptal.com/developers/gitignore/)

#### github 꾸미기 ####
나의 github 아이디와 같은 이름의 저장소를 만들면 프로필을 꾸밀 수 있다.
> github는 공유를 위한 공간, 되도록이면 clone을 통해 로컬에서 내려 받아서 작업을 하도록 하자.

나 같은 경우는 qldrh112/qldrh112를 만들고 README.md 파일을 수정하여 원격저장소에 저장하면 프로필이 꾸며진다고 한다.

#### README.md ####
- 프로젝트에 대한 설명 등을 기술하여 다른 사람이 알아 먹을 수 있고 프로젝트를 잘 운영할 수 있게 하는 것이 핵심
- 반드시 원격저장소 최상단에 위치해야 한다.


### 실습1
- a.txt와 b.txt를 담은 git_practice 파일을 github 저장소에 올린다.
- 그 후 내용 수정을 한 뒤 다시 업로드한다. 

![jpg](image.png)

### 실습2
- .txt 파일을 만들어 commit하여 원격저장소에 업로드 한다.
- 파트너에게 저장소의 권한을 주어, 파일을 clone하게 한 뒤, 그가 수정한 파일을 내가 다시 수정한다.
- 반대로도 수행한다.

![Alt text](image-1.png)

### 실습3
- 파이썬으로 학생들의 자리를 배정하는 프로그램을 만들어라
- 단, 학생이 직전에 앉았던 자리를 배정받아서는 안 된다.

*<사유과정>*
  1. 학생 수를 입력받는다.
  2. 학생 수를 인자로 하는 반복문으로 학생 수만큼의 요소를 가진 리스트를 만든다.
  3. random 모듈의 shuffle 함수로 리스트의 요소를 바꾼다.
  4. 만약...

  ```python
  import random
  NoS = int(input())
  seat = {}

  for i in range(NoS+1):
      seat[i] = str(i)
    
  tmp = list(seat.values())
  shuffled_number = random.shuffle(tmp)

  for key, value in enumerate(shuffled_number, start=1):
    try key == value:
        print(key, value)
  ```
  shuffle을 돌리면 나중에 출력했을 때, None으로 출력되었기에 다른 방법을 구상하였다.
  
  함수로 만들어 매개 변수로 학생 수를 받는다면 좀 더 편하게 움직일 수 있다고 생각했다.

  *<사유과정 ver.2>*
  1. 랜덤 모듈을 데려온다.
  2. 각 학생이 이전에 앉았던 번호를 리스트에 담는다.
  3. sample 함수로 리스트를 섞는다.
  4. enumerate로 자리 번호와 학생 번호를 딕셔너리로 받는다.
      - 만약, 이전에 앉았던 자리 번호와 새로 받는 자리의 번호가 같으면 다시 함수를 실행시킨다.
      - 그렇지 않으면 출력한다.

``` python
def random_seat(n):
    import random
    members = []
    for i in range(1, n+1):
        members.append(i)
        
    shuffled_members = random.sample(members, len(members))
    
    for key, value in enumerate(shuffled_members, start=1):
        if key == value:
            random_seat(n)
        else:
            print(f'#{key}: {value}')
        
random_seat(28)
```
  문제는 이제 출력되다가 중간에 key와 value가 같으면 깨끗하게 출력되지 않는 것이다.

우선 이거까지 하고 매일 10분은 투자해서 markdown 파일 작성을 해야겠다.