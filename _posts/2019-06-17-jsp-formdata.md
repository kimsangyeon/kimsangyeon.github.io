---
layout: post
title: "jsp form data"
categories: [ javascript, jsp ]
image: assets/images/banner/webpack.png
author: yeon
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

```java
MultipartRequest multipartRequest = new MultipartRequest(req, saveDir, maxSize, encType, new DefaultFileRenamePolicy());
let path = multipartRequest.getParameter("path");
```

<br><br>

### MultipartParser
MultipartRequest를 사용할 경우 saveDir을 서버단에서 지정한 후 request에서 multipartRequest로 꺼내는 형태여서 request에 담겨있는 path정보를 사용하기에는 조금 무리가 있었다. <br><br>

해서 Part별로 data 정보를 꺼내는 **MultipartParser**를 사용하는 방법사용 <br>

```java
MultipartParser mutipartParser = new MultipartParser(request, saveDir);
Part part;
while ((part = mutipartParser.readNextPart()) != null) {
    String name = new String(part.getName().getBytes("8859_1"), "euc-kr");

    if (part.isParam()) {
        // 파일이 아닐때
        ParamPart paramPart = (ParamPart) part;
        String value = new String(paramPart.getStringValue().getBytes("8859_1"), "euc-kr");
        out.println("param; name=" + name + ", value=" + value);
    } else if (part.isFile()) {
        // 파일일때
        FilePart filePart = (FilePart) part;
        String fileName = filePart.getFileName();
        if ( fileName != null )
            fileName = new String(filePart.getFileName().getBytes("8859_1"),"euc-kr");
        if (fileName != null) {
            long size = filePart.write　To(dir);
            out.println("file; name=" + name + "; filename=" + fileName +
            ", filePath=" + new String(filePart.getFilePath().getBytes("8859_1"),"euc-kr") +
            ", content type=" + filePart.getContentType() +
            ", size=" + size);
        } else {
            //  form type 이 file 이지만 비어있는 파라메터
            out.println("file; name=" + name + "; EMPTY");
        }
    }
}
```




<br><br><br>