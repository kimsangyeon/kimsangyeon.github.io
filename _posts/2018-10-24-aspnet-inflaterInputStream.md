---
layout: post
title: "Asp.net InflaterInputStream" 
categories: [ REST ]
image: assets/images/banner/restapi.png
author: yeon
---

# Asp.net InflaterInputStream
작업중 binary 압축 데이터를 decompress하는 작업이 필요했다.

<br>

#### ICSharpCode SharpZipLib

<br>

SharpZipLib (#ziplib, 이전의 NZipLib)은 압축 및 압축 방법, PKZIP 2.0 스타일 및 AES 암호화, GNU 긴 파일 확장명, GZip, zlib 및 raw deflate가있는 tar와 BZip2를 사용하여 Zip 파일을 지원하는 압축 라이브러리입니다. <br>
Deflate64는 아직 지원되지 않지만 Zip64는 지원됩니다. 어셈블리 (GAC에 설치 가능)로 구현되므로 다른 프로젝트 (.NET 언어로)에 쉽게 통합 될 수 있습니다. SharpZipLib를 만든 사람은 이렇게 말합니다. <br>
"gzip / zip 압축이 필요하고 libzip.dll 같은 것을 사용하고 싶지 않아서 zip 라이브러리를 C #으로 포팅했습니다. 모두 순수한 C #으로 원합니다. " 

<br><br>


```c#
using (FileStream stream = new FileStream(unzipPath, FileMode.Open, FileAccess.Read))
{
    stream.Seek(16, SeekOrigin.Begin);
    using (ICSharpCode.SharpZipLib.Zip.Compression.Streams.InflaterInputStream ifis = new ICSharpCode.SharpZipLib.Zip.Compression.Streams.InflaterInputStream(stream)) {
        int bytesLeidos = 0;

        byte[] buffer = new byte[1024];
        while ((bytesLeidos = ifis.Read(buffer, 0, buffer.Length)) > 0)
        {
            for (int i = 0; i < bytesLeidos; i++)
            {
                serializedData.Add(buffer[i] & 0xFF);
            }
        }
    }
}
```

- FileStream으로 stream 형태로 file을 읽기
- 앞 포지션 16byte 제거를 위해 Seek -> position 16으로 이동
- ICSharpCode.SharpZipLib.Zip.Compression.Streams.InflaterInputStream 사용하여 stream 변환하여 binary 압축해제


<br><br><br>