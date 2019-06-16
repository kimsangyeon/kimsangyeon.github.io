---
layout: post
title: "jsp form data"
categories: [ javascript, jsp ]
image: assets/images/banner/webpack.png
author: yeon
featured: true
---

## jsp form data
ajax로 전송된 multipart/form-data에서 전송시 form data에 담아서 보낸 path 정보를 jsp에서 꺼낼 수 없냐는 문의가 있었다. <br>
처음엔 request.getParameter로 지정한 키 값으로 데이터를 꺼내면 되지 않을까 생각 했지만 multipart/form-data 였던 것... <br>
request.getParameter("key") 호출시 null 만 리턴된다. <br>

<br>

### MultipartRequest
**Multipart Request** 사용하여 getParameter로 지정하였던 데이터 가져오기로 해결 <br>

<br>

lib폴더에 [cos.jar](http://servlets.com/cos/) 추가후 <br>

```jsp
<%@page import="com.oreilly.servlet.multipart.DefaultFileRenamePolicy"%>
<%@page import="com.oreilly.servlet.MultipartRequest"%>
```

<br>

```javascript
MultipartRequest multipartRequest = new MultipartRequest(req, saveDir, maxSize, encType, new DefaultFileRenamePolicy());
let path = multipartRequest.getParameter("path");
```

<br>

<br><br><br>