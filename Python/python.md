# Python

* [Python 공식문서](https://docs.python.org/ko/3/)
* [python 문법](https://wikidocs.net/145)
* [ *, ** 의 의미](https://sshkim.tistory.com/182)
* [ _, 언더스코어의 의미](https://doorbw.tistory.com/153)

##### 문자열치환
``` replace(old, new, [count]) -> replace("찾을값", "바꿀값", [바꿀횟수]) ```
##### 앞뒤 공백제거
``` strip() ```
##### 반복문 인덱스 구하기
``` for i in range(len(array)): ```

##### 딕셔너리리스트 검색
``` 
  list = [{'Name': 'Tom', 'Age': 30},{'Name': 'Jack', 'Age': 31},{'Name': 'Sue', 'Age': 32}]
  tom = (item for item in list if item['Name'] == 'Tom')\
  dict = next(tom, False)
  >>> dict {'Name': 'Tom', 'Age': 30} 
  >>> dict['Age']
  
  ret = next(item for item in list if item['Name'] == 'Tom'), None)
  print(ret)
```
