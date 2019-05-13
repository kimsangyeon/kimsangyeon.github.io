---
layout: post
title: "script async defer" 
categories: [ html, script, async, defer ]
image: assets/images/banner/html.png
featured: false
author: yeon
---


## HTML <script> 파싱
\<script>를 HTML 파싱중 만난다면, HTML 파싱이 중단되고 스크립트를 가져와 실행한다.
스크립트 실행 후 HTML 파싱이 다시 시작. 이는 문서 로딩을 지연시키는 이유중 하나이다.
이를 완화하기위해 HTML 파싱과 \<script> 로딩을 비동기처리 가능하도록 async, defer 속성이 있다.

### <script async>
\<script async> HTML 파싱과 병렬적(비동기)으로 가져오며, 가능할 때 즉시 실행.
스크립트가 독립적인 경우 사용 (ex analytics)

### <script defer>

\<script defer> HTML 파싱과 병렬적(비동기)으로 가져오지만, HTML 파싱이 완료된 후에
스크립트가 실행된다. \<body> 끝부분에 \<script>를 두는것과 비슷하게 동작.

async와 defer는 src 속성이 있는 \<script>에서만 동작한다.

<br><br><br>