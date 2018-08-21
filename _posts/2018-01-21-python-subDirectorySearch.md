---
layout: post
title: "Sub Directory Search 만들기"
categories: [ Python ]
author: "Yeon"
---

# Sub Directory Search 만들기

### 하위 directory를 재귀적으로 탐색

>os path를 사용하여 파일 경로를 검사하여 탐색 <br>
파일이 directory인 경우 해당경로 안쪽으로 재탐색
```python
# Sub Directory Search File
import sys, os

def search(dirName):
    fileNames = os.listdir(dirName)

    for fileName in fileNames:
        filePath = os.path.join(dirName, fileName)

        if os.path.isdir(filePath):
            search(filePath)
        else:
            ext = os.path.splitext(filePath)[1]
            if ext == '.py':
                print(filePath)

search("/Users/sangyeon/python_study")
```

> 에러 출력 함수 만들기 <br>
탐색중 Permission Error 발생하는 경우 <br>
EPERM 에러 검사하여 에러 출력하고 pass를 넣어 계속해서 탐색하도록 함.

```python
from errno import EACCES, EPERM, ENOENT

except (IOError, OSError) as e:
        exc_type, exc_obj, exc_tb = sys.exc_info()
        fileName = os.getcwd() + "/" + os.path.split(exc_tb.tb_frame.f_code.co_filename)[1]
        print_error_message(e, fileName)
        pass

def print_error_message(e, file_name):
    #PermissionError
    if e.errno == EPERM or e.errno == EACCES:
        print("PermissionError error({0}): {1} for: {2}".format(e.errno, e.strerror, file_name))
    #FileNotFoundError
    elif e.errno==ENOENT:
        print("FileNotFoundError error({0}): {1} as: {2}".format(e.errno, e.strerror, full_name))
    elif IOError:
        print("I/O error({0}): {1} as: {2}".format(e.errno, e.strerror, file_name))
    elif OSError:
        print("OS error({0}): {1} as: {2}".format(e.errno, e.strerror, file_name))
```


[참고: 하위 디렉터리 검색하기](https://wikidocs.net/39)