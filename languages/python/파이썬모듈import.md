# Python import sys.path

- 파이썬 모듈을 import 할 수 없거나, 엉뚱하게 동작하는 일들이 생김

### sys.path
- 모듈을 import 할 때 모듈을 찾아야할 경로들을 저장한 list
- 해당 리스트 directory 경로 아래서 모듈을 찾아 import

- sys.path가 만들어지는 과정
```
1. 최초 실행된 **python 스크립트가 위치한 디렉토리** add
2. 환경 변수 중 PYTHONPATH 값 가져옴
3. OS 나 python 배포판이 설정해 둔 값 더함
```

- 해당 경로의 하위에 모듈이 없을 경우 `ModuleNotFound`

- 예시)
- 파일 경로
	- /Users/lsy/workspace/temp/main.py
	- /Users/lsy/workspace/temp/module_demo/library.py
	- /Users/lsy/workspace/temp/module_demo/util.py
```
.
├── main.py
└── module_demo
    ├── library.py
    └── util.py
```


- main.py
```python
import sys

print("sys path from main.py")
print("\n".join(sys.path))

print("__name__ of main.py")
print(__name__)
```
- pwd
	- /Users/lsy/workspace/temp
- 수행결과
``` 
sys path from main.py
/Users/lsy/workspace/temp
/Users/lsy/.pyenv/versions/3.10.5/lib/python310.zip
/Users/lsy/.pyenv/versions/3.10.5/lib/python3.10
/Users/lsy/.pyenv/versions/3.10.5/lib/python3.10/lib-dynload
/Users/lsy/.pyenv/versions/3.10.5/lib/python3.10/site-packages
__name__ of main.py
__main__
```
- 첫번째 줄을 보면 script가 수행된 경로의 path가 추가되었다.

### 문제점 
- main.py 코드
```python
import sys

print("sys path from main.py")
print("\n".join(sys.path))

print("__name__ of main.py")
print(__name__)

from module_demo import library
from module_demo import util

```
- util.py 의 코드
```python
import sys

print('sys.path from util.py')
print('\n'.join(sys.path))
print()

  
print('__name__ of util.py')
print(__name__)
print()


import library
```
- main.py 코드를 수행시켰을 때,
-util 코드의 import library 코드에서 ModuleNotFound 오류 발생
-> main 의 path 디렉토리 안에서 libary 모듈을 찾을 수 없기 때문!


### 해결책
- relative import 를 사용 
```
import library -> from . import library
```
- 해당 파일을 import 할 때, 현재 자기와 같은 위치에 있다고 알려줌

**단, util을 직접 실행할 경우, 다른 오류가 발생**
```
Traceback (most recent call last):
  File "/Users/lsy/workspace/temp/module_demo/util.py", line 11, in <module>
    from . import library
ImportError: attempted relative import with no known parent package
```
**- 어떤 스크립트를 모듈로 사용할지 아니면 직접 실행할지 구성 해야함!**

- 내가 생각해본 방식
``` python
if __name__ == "__main__":
    import library
else:
    from . import library
```

- 모듈로 동작할때와 스크립트로 동작할때를 다르게 동작하도록..?
