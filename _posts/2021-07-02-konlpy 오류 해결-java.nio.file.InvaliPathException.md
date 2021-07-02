# konlpy 오류해결-java.nio.file.InvaliPathException

jdk, Jpype, konlpy를 주피터 노트북에 설치 후 실행 테스트를 하려고 했는데 오류가 발생하였다. 
```python
from konlpy.tag import Kkma
kkma = Kkma()

print(kkma.sentences('한국어의 문장 분석. konlpy를 이용합니다.'))
#한글 사전에 있는 단어만 추출
print(kkma.nouns('한국어의 문장 분석. konlpy를 이용합니다.'))
#형태소 분석 - 단어별로 분할을 해서 품사와 함께 리턴
print(kkma.pos('한국어의 문장 분석. konlpy를 이용합니다.'))
```
![](https://i.imgur.com/60zNvP0.png)

**해결방법**
konlpy 패키지가 설치되어 있는 폴더에 가면 jvm.py 파일이 있는데 소스코드를 수정하고 커널을 리스타트해서 테스트한다.

![](https://i.imgur.com/cY8az1k.png)

**결과**
![](https://i.imgur.com/ivamNfA.png)





