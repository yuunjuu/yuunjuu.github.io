---
title: "[Git] SSH KEY로 2개 이상의 Git 계정 관리하기"
excerpt: "SSH KEY를 이용하여 한 대의 컴퓨터에서 2개 이상의 Git 계정 관리하기"

categories:
  - Git
tags:
  - [Git, SSH]

toc: true
toc_sticky: true

date: 2021-10-02
last_modified_at: 2021-10-02
---

# 작업환경
- Windows 10
- Git bash


# 1. 계정별 SSH KEY 생성
---
우선 github 계정 2개가 준비된 상태에서 Git bash를 실행하고 ~/.ssh로 이동한다.
```
$ cd ~/.ssh
```
**1) (생략 가능)기존의 id_rsa 파일 삭제**

~/.ssh 내부에 id_rsa 파일이 존재하는지 확인하고 있다면 해당 파일을 삭제한다. 만약 id_rsa 파일이 존재하지 않는다면 이 단계는 생략한다.
```
$ ls -al
$ rm ~/.ssh/id*
```
**2) 계정별 SSH 키 생성**

아래 명령어를 통해 계정별 SSH 키를 생성한다.
```
$ ssh-keygen -t rsa -C "계정1 이메일" -f "id_rsa_계정1"
$ ssh-keygen -t rsa -C "계정2 이메일" -f "id_rsa_계정2"
```
위 명령어를 입력하면 아래와 같은 문장이 나타나고, 보안상 passphrase를 입력하라는 문장이 나타난다. 설정하지 않으려면 엔터를 2번 치면 된다.
```
**config 파일 생성 및 내용 입력**

Generating public/private rsa key pair.
Enter passphrase(empty for no passphrase):

```
성공적으로 생성되면 아래 4개의 파일이 생성된다.
- id_rsa_계정1
  
- id_rsa_계정1.pub
  
- id_rsa_계정2
  
- id_rsa_계정2.pub


# 2. SSH 키 복사
---
public key를 복사한다.
```
$ cat ~/.ssh/id_rsa_계정1.pub
$ cat ~/.ssh/id_rsa_계정1.pub
```
복사한 각각의 키를 해당 계정 SSH KEY에 등록한다.
1. github 계정 로그인 > 'Settings'로 이동
   
2. 좌측 탭의 'SSH and GPG keys'로 이동
   
3. 'SSH keys'의 'New SSH key' 클릭 > 복사한 SSH public key 붙여넣기


# 3. SSH config 작성
---
SSH profile을 관리해주는 ~/.ssh에서 config 파일을 생성하고 vim을 이용하여 파일 내용을 작성한다.
```
$ touch config
$ vi config
```
config 파일에는 다음과 같은 내용을 작성한다.
```
# 계정1 account
Host github.com-계정1
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_rsa_계정1

# 계정2 account
Host github.com-계정2
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_rsa_계정2
```


# 4. 연결 테스트
---
- github에서 테스트할 repository를 생성한다.
   
- 원하는 위치에 클론을 할 폴더를 생성한다.
   
- Git Bash에서 폴더 경로로 이동한다.

Git을 초기화한 후 테스트 repository의 SSH를 복사하고, ssh config에서 작성한 'Host'로 입력하여 클론(clone)한다.
```
$ git init
$ git clone git@github.com-계정1:계정1/repo이름.git
```
클론한 경로로 이동하여 아래 과정을 통해 커밋 테스트를 한다.
```
$ touch test.txt
$ vi test.txt
$ git add test.txt
$ git commit -m "test"
$ git push
```
이 과정을 마치면 생성한 test.txt 파일이 github repository에 push된 것을 확인할 수 있다.

