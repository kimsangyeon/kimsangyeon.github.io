---
layout: post
title: "Github Fork Repository 동기화" 
categories: [ git, fork, remote ]
image: assets/images/banner/github.png
author: yeon
---


### Github Fork Repository 동기화
오픈소스 Repository 최신으로 동기화 시키기

- Open Source Repository에 지속적으로 contribution 할때
- fork Repository를 원본 Repository 업데이트 사항을 받아올때

<br><br><br>

#### Fork Repository에서 Remote Repository 확인
~~~
git remote -v
origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
~~~

<br><br>

#### 원본 Repository를 remote에 추가
~~~
git remote add upstream
https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
~~~

<br>

##### 추가된 remote 확인
~~~
git remote -v
origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (fetch)
upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (push)
~~~

<br><br>

#### 최신 업데이트 가져오기
~~~
git fetch upstream
remote: Counting objects: 75, done.
remote: Compressing objects: 100% (53/53), done.
remote: Total 62 (delta 27), reused 44 (delta 9)
Unpacking objects: 100% (62/62), done.
From https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY
 * [new branch]      master     -> upstream/master
~~~

<br><br>

#### upstream Repository를 Fork Repository로 merge
~~~
git checkout master
Switched to branch 'master'

$ git merge upstream/master
Updating a422352..5fdff0f
Fast-forward
 README                    |    9 -------
 README.md                 |    7 ++++++
 2 files changed, 7 insertions(+), 9 deletions(-)
 delete mode 100644 README
 create mode 100644 README.md
~~~

<br>

##### merge된 branck push
~~~
git push origin master
~~~

<br><br><br>