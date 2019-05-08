---
layout: post
title: "Github issue 만들기 & pull request" 
categories: [ git, github ]
image: assets/images/banner/github.png
author: yeon
---


### Github issue 만들어보기 #1
Github repository를 좀 더 체계적으로 관리해보기위해 이슈 만들기에 도전!


<br>

![github issue Image]({{ site.baseurl }}/assets/images/github-issue-1.png)

<br>

개인 repository에서 issues 탭으로 이동하면, 초록색 버튼 New issue를 쉽게 찾을 수 있다.

<br><br>

이슈 생성시에 오른쪽에 Assignees

![github issue Image]({{ site.baseurl }}/assets/images/github-issue-3.png)

<br>

그리고 labels를 설정 할 수 있다.

![github issue Image]({{ site.baseurl }}/assets/images/github-issue-4.png)

<br>

labels는 8가지가 기본으로 제공되며 edit label로 새로운 label 추가도 가능하다.

1. bug: 버그
2. duplicate: 중복 이슈
3. enhancement: 기능 추가
4. good first issue: 새로운이의 좋은 이슈?
5. help wanted: 도움 요청
6. invalid: 무효의, 이슈아님
7. question: 질문
8. wontfix: 대응하지 않는 이슈

<br>

New issue에서 Title 및 간단한 내용 작성후 Submit new issue 클릭!

<br><br>

![github issue Image]({{ site.baseurl }}/assets/images/github-issue-2.png)

<br>

멋지게 open으로 이슈가 생성된다.

<br><br><br>

#### Github pull request 날리기 #2
생성한 이슈에 대응되게 pull request 날리기도 해보았다.
이슈 이름과 같게 comment title 작성후 push된 새로운 branch로 pull request 탭에서 compare & pull request 생성

<br>

![github issue Image]({{ site.baseurl }}/assets/images/github-pullrequest-1.png)

<br><br>

pull request에서도 issue에서와 동일하게 assignees와 label을 설정

<br>

![github issue Image]({{ site.baseurl }}/assets/images/github-pullrequest-2.png)

<br><br>

issue와 연결되게하여 issue를 merge와 동시에 close하는 법으로 resolve: #이슈번호 comment시 issue가 자동적으로 close된다.

<br>

![github issue Image]({{ site.baseurl }}/assets/images/github-pullrequest-3.png)

<br><br>

여담으로 스크린샷 찍고 하나하나 진행하다 develop branch로 merge를 해야하는데, 실수로 master branch로 merge를 해버려서 revert 했더니

<br>

![github issue Image]({{ site.baseurl }}/assets/images/github-pullrequest-4.png)

<br>

요런식으로 pull request가 Revert형태로 다시 생성되었다.


<br><br><br>