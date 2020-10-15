Python 코딩 표준 PEP-8 훌터보기
-------------------------------

여러분이 작성하는 Python program의 가독성을 올리기 위하여 code를 정확하게 포맷팅할 수 있는 Python style 지침 PEP-8에 대하여 빠르고 쉽게 배울 수 있도록 [PEP-8 Tutorial: Code Standard in Python](https://www.datacamp.com/community/tutorials/pep8-tutorial-python-code)를 번역하였다.

PEP(Python Enhancement Proposal)-8은 Python code를 보다 읽기 쉽고 체계적으로 작성하는데 필요한 사항을 기술하고 있다. Python 창시자인 Guido Van Rossum은 "code는 작성하는 것 보다 훨씬 많이 읽힌다"고 하였다.

이 글에서는 code 예를 들어가며 PEP-8를 설명하며 아래의 토픽을 다룰 것이다.

* 먼저 PEP-8이 무엇이며 왜 필요한 가에 대하여 [소개](#intro)한다.
* 다음, 프로그래머들이 많은 관심을 보이고 있는 [들여쓰기(indentation)](#indent)을 다룬다. 탭(tab) 또는 빈칸(space)중 무엇을 사용하여야 하는지 그 답을 구할 수 있을 것이다.
* 무시해도 되지만, 최대 라인 수[(maximum line length)](#maxlinelength)에 대한 가이드 라인(guide line)도 있다.
* 또한, 빈줄(blank line)을 다루는 방법도 제안한다.
* 그리고 [식(expression)과 문장(statement)에 있는 빈칸(whitespace)](#whitespace)에 대한 사용을 초보자도 쉽게 적용할 수 있다.
* Python으로 프로그래밍을 할 떄 인코딩이 무엇이며 왜 필요할까? Python3에서 디폴트(default)는 무엇인가 [소스 라인 인코딩 (source line encoding)](#sourceline)에서 이들을 설명한다.
* 코딩할 때 [import문](#import)은 자주 사용된다. import문의 순서, 절대(absolute)와 상대(relative) import문, 그리고 와일드카드(wildcard) import 등에 대하여도 설명할 것이다.
* 문서화(documentaton)는 응용의 기능 추적과 최종 산출물의 전체적인 품질 향상에 필수이다. 이를 위하여 [주석(comment)](#comment)은 매우 중요하다.
* 다음, 프로그래머들이 많은 관심을 보이고 있는 [들여쓰기(indentation)](#indent)을 다룬다. 탭(tab) 또는 빈칸(space)중 무엇을 사용하여야 하는지 그 답을 구할 수 있을 것이다.* 바라지 않을 수도 있겠지만, 최대 라인 수[(maximum line length)](#maxlinelength)에 대한 가이드라인(guideline)도 있다.* 또한, 빈줄(blank line)을 다루는 방법을 제안한다.* 그리고 [식(expression)과 문장(statement)에 있는 빈칸(whitespace)](#whitespace)는 초보자도 쉽게 사용요할 수 있다.* Python으로 프로그래밍을 할 떄 인코딩이 무엇이며 왜 필요할까? Python3에서 디폴트(default)은 무엇인가 [소스 라인 인코딩 (source line encoding)](#sourceline)에서 이들을 설명한다.* 코딩할 때 [import문](#import)은 자주 사용된다. import문의 순서, 절대(absolute)와 상대(relative) import문, 그리고 와일드카드(wildcard) import 등에 대하여 다룰 것이다.* 문서화(documentaton)는 응용의 기능 추적과 최종 산출물의 전체적인 품질 향상에 필수이다. 이를 위하여 [주석(comment)](#comment)은 매우 중요하다.
이 글에서는 code 예를 들어가며 PEP-8를 설명하며 아래의 토픽을 다룰 것이다.* 먼저 PEP-8이 무엇이며 왜 필요한 가에 대하여 [소개](#intro)한다.* 다음, 프로그래머들이 많은 관심을 보이고 있는 [들여쓰기(indentation)](#indent)을 다룬다. 탭(tab) 또는 빈칸(space)중 무엇을 사용하여야 하느지에 대한 답을 구할 수 있을 것이다.* 바라지 않을 수도 있겠지만, 최대 라인 수[(maximum line length)](#maxlinelength)에 대한 가이드라인(guideline)도 있다.* 또한, 빈줄(blank line)을 다루는 방법을 제안한다.* 그리고 [식(expression)과 문장(statement)에 있는 빈칸(whitespace)](#whitespace)는 초보자도 쉽게 사용요할 수 있다.* Python으로 프로그래밍을 할 떄 인코딩이 무엇이며 왜 필요할까? Python3에서 디폴트(default)은 무엇인가 [소스 라인 인코딩 (source line encoding)](#sourceline)에서 이들을 설명한다.* 코딩할 때 [import문](#import)은 자주 사용된다. import문의 순서, 절대(absolute)와 상대(relative) import문, 그리고 와일드카드(wildcard) import 등에 대하여 다룰 것이다.* 문서화(documentaton)는 응용의 기능 추적과 최종 산출물의 전체적인 품질 향상에 필수이다. 이를 위하여 [주석(comment)](#comment)은 매우 중요하다.

<a name="intro"></a>

### PEP-8 소개

Python은 최근 몇년 동안 확산되어 널리 사용되는 프로그램잉 언어로 자리 잡았다. 비교적 쉽게 배울 수 있다. 프로그래밍 언어의 사용성을 높이는 다양한 오픈 소스 모듈을 제공하며, 특히 데이터 과학 (Data Science)와 웹 프로그래밍 공동체로부터 각광을 받고 있다.

그러나 Python code를 바람직하게 작성하여야 Python의 장점을 살릴 수 있다. <code>import this</code>를 수행하여 볼 수 있는 목표를 염두에 두고 Python을 만들었다.

```pyrhon
import this
```

```
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```

위에서 열거한 20 문장은 Python 프로그래밍에서 사용하는 원칙이다. 위 결과에서 "Readability Counts"가 코드를 작성할 떄 주로 주의를 기울여야 할 부분이다. 즉 프로그래머 또는 데이터 과학자가 이를 이해하여 주어진 문제를 해결하는 코드로 기여할 수 있어야 한다.

다음 절들에서 위 사항들을 어떻게 달성할 수 있는 가 살펴본다.

<a name="indent"></a>

### 들여쓰기(Indentation)

Python 프로그래밍에서 정확히 들여쓰기 기능을 이용하여야 한다. 그러나 구문 오류 (syntax error)를 유발할 수 있으므로 조심하여야 한다. 그리하여 4칸 들여쓰기를 권장한다. 예를 들면 아래 예는 4칸 들여쓰기를 사용한 것이다.

```python
if True:
    print("IF works")
```

아래와 같이 <code>print</code>문이 있는 <code>for</code> 루프에서도 4칸 들여쓰기를 한다.

```python
for element in range(0, 5):
    print(element)
```

수식이 길때 식을 세로로 정렬한다. 이를 위하여 "내어쓰기(hanging indent)"를 사용한다. 긴 수식 작성을 위하여 내어쓰기 몇몇 다른 예는 아래와 같다.

```python
value = square_of_numbers(num1, num2,
                       num3, num4)
```

```python
def square_of_number(
    num1, num2, num3,
    num4):
return num1**2, num2**2, num3**2, num4**2
```

```python
value = square_of_numbers(
    num1, num2,
    num3, num4)
```

```python
list_of_people = [
    "Rama",
    "John",
    "Shiva"
]
```

```python
dict_of_people_ages = {
    "ram": 25,
    "john": 29,
    "shiva": 26
}
```

대부분의 개발자들은 들여쓰기를 할때 텝을 사용할 것인가 또는 빈칸을 사용할 것인가에 대하여 의문을 갖는다. 개발자 공동체에서 텝과 빈칸의 차이에 대하여 논의하고 있다. (예로 [문서](https://stackoverflow.blog/2017/06/15/developers-use-spaces-make-money-use-tabs/)가 있다.) 일반적으로 코딩할 때 빈칸을 사용한 개발자들은 탭 대신 들려쓰기에 빈칸 사용을 선호하며, 그렇지 않을 경우 프로그램의 들여쓰기를 변경하여야 한다. Python 3에서는 들여쓰기로 빈칸과 탬을 혼용할 수 없다. 이점 유의하여야 하며 이때문에 탬과 빈칸 중 하나를 선택하여야 한다.

<a name="maxlinelength"></a>

### 한 문장의 최대 길이(Maximum Line Length)

Python 프로그램을 작성할 떄 일반적으로 최대 79 글자로 한 문장을 작성하도록 하고 있다. 이렇게 하는 것이 좋은 이유는 아래와 같다.* 프로그램 파일을 옆에 놓고 비교할 수 있다.* 코드를 보다 쉽게 읽고 잘 이해하기 위하여 수평으로 이동할 필요없이 식을 볼 수 있다.

주석은 72 글자로 작성하여야 한다. (뒤에 주석 작성을 위한 통상적인 규약에 대하여 살펴 볼 것이다.) 결국, 작은 그룹으로 소프트웨어를 개발하고 최대길이 지침을 변경하는 것을 대부분의 개발자들이 동의한다면 사용할 코딩 규약과 스타일을 정하는 것은 개발자 자신들의 몫이다. 그러나 오픈소스 프로젝트에 기여하려면 PEP-8에서 정한 최대길이 규칙을 따라야 할 필요가 있다.

예를 들면, 연산자 <code>\+</code> 를 사용할 때, 이해하기 쉬운 코드를 위하여 적절한 줄바꾸기(line break)를 사용하여야 한다.

```python
total = (A
         +   B
         +   C)
```

보다는

```python
total = (A +
         B +
         C)
```

또는

```python
total = A
        + B
        + C
```

이 바람직하다.

줄여서 일관되게 이진 연산자 (binary operator) 앞 또는 뒤에 줄 바꿈을 추가한다. 만약 새롭게 코드를 작성한다면 위의 마지막 방법을 추천한다. 즉 이진 연산자 앞에서 줄 바꾸기를 하는 것이다.

<a name="blankline"></a>

### 빈 줄(Blank Lines)

Python 코드를 작성할 때에는 아래의 예와 같이, 최상위 함수 (top-level function)과 클라스(class)는 2줄을 띠어 분리한다. 클래스 내의 메소드(method)는 한 줄 띠어 정의한다.

```python
class SwapTestSuite(unittest.TestCase):
    """
        Swap Operation Test Case
    """

    def setUp(self):
        self.a = 1
        self.b = 2

    def test_swap_operations(self):
        instance = Swap(self.a,self.b)
        value1, value2 =instance.get_swap_values()
        self.assertEqual(self.a, value2)
        self.assertEqual(self.b, value1)


class OddOrEvenTestSuite(unittest.TestCase):
    """
        This is the Odd or Even Test case Suite
    """
    def setUp(self):
        self.value1 = 1
        self.value2 = 2

    def test_odd_even_operations(self):
        instance1 = OddOrEven(self.value1)
        instance2 = OddOrEven(self.value2)
        message1 = instance1.get_odd_or_even()
        message2 = instance2.get_odd_or_even()
        self.assertEqual(message1, 'Odd')
        self.assertEqual(message2, 'Even')
```

위에서 볼 수 있듯이 2줄로 클래스 <code>SwapTestSuite</code>와 <code>OddOrEvenTestSuite</code>를 분리하며, 메소드 <code>.setUp()</code>과 <code>.test_swap_operations()</code>는 1줄로 분리되어 있다.

<a name="whitespace"></a>

### 문과 식에서 빈 칸(Whitespaces in Expressions and Statements)

코드에 빈 칸을 사용할 때 바람직한 예는 아래와 같다.

<table>
  <tr>
    <th><div align="center"> 바람직한 사용 예</div></th>
    <th><div align="center"> 피하여야 하는 사용 예</div></th>
  </tr>
  <tr>
    <td><div align="left">func(data, {pivot: 4})</div></td>
    <td><div align="left">func( data, { pivot: 4 } )</div></td>
  </tr>
  <tr>
    <td><div align="left">indexes = (0,)</div></td>
    <td><div align="left">indexes = (0, )</div></td>
  </tr>
  <tr>
    <td><div align="left">if x == 4: print x, y; x, y = y</div></td>
    <td><div align="left">if x == 4 : print x , y ; x , y = y , x</div></td>
  </tr>
  <tr>
    <td><div align="left">spam(1)</div></td>
    <td><div align="left">spam (1)</div></td>
  </tr>
  <tr>
    <td><div align="left">dct['key'] = lst[index]</div></td>
    <td><div align="left">dct ['key'] = lst [index]</div></td>
  </tr>
  <tr>
    <td><div align="left">x = 1<br>y = 2<br>long_variable = 3</div></td>
    <td><div align="left">x = &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 1<br>
    y = &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 2<br>long_variable = 3</div></td>
  </tr>
  <tr>
    <td><div align="left">ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]<br>
                          ham[lower:upper], ham[lower:upper:], ham[lower::step]<br>
                          ham[lower+offset : upper+offset]<br>
                          ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]<br>
                          ham[lower + offset : upper + offset]</div></td>
    <td><div align="left">ham[lower + offset:upper + offset]<br>
                          ham[1: 9], ham[1 :9], ham[1:9 :3]<br>
                          ham[lower : : upper]<br>
                          ham[ : upper]</div></td>
  </tr>
  <tr>
    <td><div align="left">i = i + 1<br>
                          submitted += 1<br>
                          x = x2 - 1<br>
                          hypot2 = xx + yy<br>
                          c = (a+b) (a-b)</div></td>
    <td><div align="left">i=i+1<br>
                          submitted +=1<br>
                          x = x  2 - 1<br>
                          hypot2 = x  x + y  y<br>
                          c = (a + b)  (a - b)</div></td>
  </tr>
  <tr>
    <td><div align="left">def complex(real, imag=0.0):<br>
                          &emsp; &emsp; return magic(r=real, i=imag)</div></td>
    <td><div align="left">def complex(real, imag = 0.0):<br>
                          &emsp; &emsp; return magic(r = real, i = imag)</div></td>
  </tr>
  <tr>
    <td><div align="left">def munge(input: AnyStr): ...<br>
                          def munge() -> AnyStr: ...</div></td>
    <td><div align="left">def munge(input:AnyStr): ... <br>
                          def munge()->PosInt: ...</div></td>
  </tr>
  <tr>
    <td><div align="left">def munge(sep: AnyStr = None): ...<br>
                          def munge(input: AnyStr, sep: AnyStr = None, limit=1000): ...</div></td>
    <td><div align="left">def munge(input: AnyStr=None): ...<br>
                          def munge(input: AnyStr, limit = 1000): ...</div></td>
  </tr>
  <tr>
    <td rowspan="4"><div align="left">if foo == 'blah':<br>
                          &emsp; &emsp; do_blah_thing()<br>
                          do_one()<br>
                          do_two()<br>
                          do_three()</div></td>
  </tr>
  <tr>
    <td><div align="left">if foo == 'blah': do_blah_thing()<br>
                          do_one(); do_two(); do_three()</div><br></td>
  </tr>
  <tr>
    <td><div align="left">if foo == 'blah': do_blah_thing()<br>
                          for x in lst: total += x<br>
                          while t &lt; 10: t = delay()</div><br></td>
  </tr>
  <tr>
    <td><div align="left">if foo == 'blah': do_blah_thing()<br>
                          else: do_non_blah_thing()<br><br>
                          try: something()<br>
                          finally: cleanup()<br><br>
                          do_one(); do_two(); do_three(long, argument,list, like, this)<br><br>
                          if foo == 'blah': one(); two(); three()</div></td>
  </tr>
  <tr>
    <td><div align="left">FILES = ('setup.cfg',)</div></td>
    <td><div align="left">FILES = 'setup.cfg',</div></td>
  </tr>
  <tr>
    <td><div align="left">FILES = [<br>
                          &emsp; &emsp;'setup.cfg',<br>
                          &emsp; &emsp;'tox.ini',<br>
                          ]<br>
                          initialize(FILES,<br>
                          &emsp; &emsp; &emsp; &emsp; error=True,<br>
                          &emsp; &emsp; &emsp; &emsp;)</div></td>
    <td><div align="left">FILES = ['setup.cfg', 'tox.ini',]<br>
                          initialize(FILES, error=True,)</div></td>
  </tr>
</table>

<a name="encoding"></a>

### 소스 파일 인코딩 (Source File Encoding)

컴퓨터에는 "문자(letters)", "수(numbers)", "그림(pictures)" 등이 보여지는 형태로 저장되지 않고 이진 값인 비트로 저장된다. 즉 1 과 0 값들로 표시한다. 무언가를 나타내기 위하여 비트를 사용하기 위하여 규칙이 필요하다. 즉 인코딩 방법을 통하여 비트들을 글자, 수, 그림으로 변환하다. ASCII, UTF-8 등이 인코딩 방법의 예이다.* American Standard Code for Information Interchange (ASCII)는 컴퓨터와 인터넷에서 텍스트 파일을 위한 가장 보편적인 포맷이다. 문자, 숫자, 특수 문자 각각을 7-비트 이진수로 이 타입 파일에 저장한다.* Unicode Worldwide Character Standard 줄여 Unicode는 세계에 현존하는 여러 언어의 글자를 교환, 처리 및 표시하기 위한 방법이다. 즉, Unicode는 세상에 현존하는 필기 시스템을 수용할 수 있도록 제안되었다. Unicode 문자들을 표시하기 위하여 현재 UTF-8, UTF-16, UTF-32 인코딩 표준이 있다. - UTF-16은 Unicode 가변 길이 인코딩으로 하나 또는 두 16-비트 코드 단위로 코드 포인트를 인코드한다. - UTF-8은 다른 또 하나의 Unicode 가변 길이 인코딩으로 네 8-비트 바이트까지 사용한다. - UTF-32는 Unicode 코드 포인트당 32 비트를 사용하는 고정 길이 인코딩 밥법이다.

인코딩에 대한 보다 자세한 내용은 [이 문서](http://kunststube.net/encoding/)를 참조.

인코딩이 중요한 이유들어 보자. string은 Python에서 가장 보편적으로 사용되는 자료형(data type)중 하나이다. 표준 ASCII로 표현할 없는 문자를 포함하거나 이들로 만들어진 문자열(string)을 사용할 경우가 있을 수 있다. 결국, á, ž, ç 등과 같이 액센트 부호가 있는 문자가 있는 텍스트를 다루어야 하기 때문이다.

Python3는 기본적인 코딩으로 UTF-8을 채택하고 있다. 그러나 Python 2에서는 ASCII이다.

만약 "Flügel"과 같은 ACII가 아닌 문자를 포함하는 문자열이 있다면 어떻게 처리할까? Python2에서 문자열을 다음과 같이 참조할 수 있다.

```
>>> s
'Fl\xfcgel'
```

문자열처럼 보이지 않지만 print하면 아래처럼 보여진다.

```python
>>> print(s)
Flügel
```

print는 변수가 가리키는 값을 출력한다. ACII가 아닌 문자 ÃŒ가 인코드되고, 문자열을 참조하면 \xfc로 표시된다. string 메소드 <code>.encode()</code>와 <code>.decode()</code>를 사용하여 이를 다룰 수 있다. <code>.encode()</code>는 이미 한 방법으로 인코딩되어 있는 Unicode 문자열을 8-비트 문자열로 변환하며 <code>.decode()</code>는 주어진 인코딩으로 문자열로 변환한다.

<a name="import"></a>

### Import 문

Python 프로그래밍에서 라이브러리(library) 또는 모듈(module)을 사용하기 위하여 import문에서 이를 지정한다. 이미 알고 있는 것처럼 import문으로 프로그램을 시작한다. import문이 다수 일때 한 줄에 import문 하나씩 사용하여야 한다. 아래 예를 보면 보다 쉽게 이해할 수 있다.

<table>
  <tr>
    <th><div align="center"> 바람직한 사용 예</div></th>
    <th><div align="center"> 피하여야 하는 사용 예</div></th>
  </tr>
  <tr>
    <td><div align="left">from config import settings</div></td>
    <td rowspan="4"><div align="left">import os, sys</div></td>
  </tr>
  <tr>
    <td><div align="center">or</div></td>
  </tr>
  <tr>
    <td><div align="left">import os<br>
                          import sys</div></td>
  </tr>
</table>

라이브러리를 지정하기 위하여 import문을 사용할 때 지켜야 할 순서가 있다. 일반적으로 아래 순서를 따른다. 1. 표준 라이브러리 import문 2. 다른 커뮤니티에서 개발한 모듈/라이브러리 import문 3. 로컬 응용(application)/라이브러리 import문

#### 절대와 상대 import문 (Absolute and Relative Imports)

절대와 상대 import문의 차이에 대하여 알아본다. Python에서는 가독성을 높이기 위하여 일반적으로 절대 import문을 선호한다. 프로그램이 복잡해 짐에 따라 상대 import문을 사용하기도 한다. 암묵적인 상대 import문을 사용하지 말아야 하며 특히 Python3에서는 더 이상 지원하지 않는다. 그러면 절대와 상대 import문은 무엇일까? - 절대 import문은 함수 또는 클래스의 절대 경로(path)를 지정한다. 예를 들면

```python
import sklearn.linear_model.LogisticRegression
```

상대 import문은 Python 프로그램 파일이 있는 현재 폴더(folder)로 부터 상대 경로를 지정한다. 수행하는 프로젝트가 커짐에 따라 사용하여 프로젝트 구조를 이해하기 쉽도록 한다. 즉 아래와 같이 프로젝트를 구성하였다면,

```
.
  ├── __init__.py
  ├── __init__.pyc
  ├── __pycache__
  │   ├── __init__.cpython-35.pyc
  │   ├── bubble_sort.cpython-35.pyc
  │   ├── selection_sort.cpython-35.pyc
  ├── bubble_sort.py
  ├── heap_sort.py
  ├── insertion_sort.py
  ├── insertion_sort.pyc
  ├── merge_sort.py
  ├── merge_sort.pyc
  ├── quick_sort.py
  ├── radix_sort.py
  ├── selection_sort.py
  ├── selection_sort.pyc
  ├── shell_sort.py
  ├── tests
  │   ├── test1.py
```

프로그램 <code>test1.py</code>에서 <code>bubble_sort.py</code>에 정의된 버블 정렬 알고리즘 (bubble sort algorithm) <code>BubbleSort</code>을 import하기 위하여 상대 import문을 사용할 수 있다.

```python
from ..bubble_sort import BubbleSort
```

[이문서](https://docs.python.org/2.5/whatsnew/pep-328.html)는 절대와 상대 import문에 대하여 보다 자세히 설명하고 있다.

#### import문에서 와일드 카드 사용 (Wildcard Imports)

끝으로 모듈에서 사용되는 클래스, 메소드 또는 변수를 볼 수 없으므로 즉, 가독성을 해치므로 가급적 import문에 와일드 카드(\*) 사용을 피하여야 한다.

```python
from scikit import *
```

<a name="comment"></a>

### 주석(Comments)

Python에서 코드내의 문서화를 위하여 주석을 사용한다. 주석을 통하여 코드를 보다 잘 이해할 수 있다. 작성한 모듈을 기술하기 위하여 주석과 docstrings와 같이 문서생성에 사용할 수 있는 도구들이 있다. 자세하게 주석을 작성하여 다른 사람들이 코드를 읽고 정확히 이해하고 다른 곳에서 어떻게 사용되고 있는 지를 알 수 있어야 한다.

주석은 문자 "#"로 시작한다. 인터프리터는 해시태그(hashtag) 이후에 나타나는 문자들를 수행하지 않는다. 예를 들면, 아래 프로그램의 수행 결과이다

```python
# This is a Python single line comment
print("This is a Python comment")
```

```
"This is a Python comment"
```

이전에 설명했듯이 주석은 한줄에 72자를 넘을 수 없다.

주석을 3 방법으로 사용할 수 있다. - 블럭 주석(block comment)를 사용하여 다른 사람들에게 복잡하고 익숙하지 않은 코드를 설명할 수 있다. 긴(longer-form) 주석이 이에 해당되며, 일반적으로 주석 뒤에 나타나는 코드 일부분 또는 전체를 기술한다. 블럭 주석은 코드와 같은 수준(level)로 들여 쓰기를 한다. 블럭 주석의 각 행(line)은 #와 빈칸으로 시작한다. 주석이 한 문단 이상이면 "#"만 있는 빈 행으로 문단을 구분한다.

다음은 주석을 사용하는 예를 보이기 위하여 <code>scikit-learn</code> 라이브러리에서 발췌한 것이다.

```python
   if Gram is None or Gram is False:
        Gram = None
        if copy_X:
            # force copy. setting the array to be fortran-ordered
            # speeds up the calculation of the (partial) Gram matrix
            # and allows to easily swap columns
            X = X.copy('F')
```

-	인라인 주석이 코드의 일부분을 설명하는데 효과적이지만 그 사용을 아껴야 한다. 그러나 인라인 주석은 코드의 지정된 행이 무엇을 하는가를 기억하는 데에 도움을 줄 수 있으며 코드 전체 익숙하지 않은 개발자와 협업할 경우에도 편리할 수 있다. 인라인 주석은 코드에 이어 같은 행에 사용한다. 이 주석도 #와 빈칸으로 시작한다.

예를 들면

```python
 counter = 0  # initialize the counter
```

-	공개할 모듈 (public module), 파일, 클래스과 메소드 시작에 문서 문자열 또는 docstring을 작성한다. """로 시작하고 """로 맺는다.

```python
    """
        This module is intended to provide functions for scientific computing
    """
```

<a name="dunder"></a>

### 모듈 수준의 명명 (Module Level dunder Names)

docstring에 대하여 알아 보았다. 이제 Python에서 매우 효과적인 모듈 수준 던더(dunder) 또는 앞과 뒤에 2 밑줄 문자를 갖는 이름에 대하여도 알아야 한다. 이는 Python에서 정의된 특수한 이름으로 사용자가 정의한 함수 또는 이름과 충돌을 피하려는 것이다. [이 문서](https://shahriar.svbtle.com/underscores-in-python)에 보다 자세한 사항을 기술하였다.

\(\_\_all\_\_, \_\_author\_\_, \_\_version\_\_)같은 모듈 수준 던더는 모듈의 메인 docstring에 그리고 모든 import문 앞에 있어야 한다. docsting을 제외하고 코드 맨 처음에 "<code>from \_\_future\_\_</code>" import문에서 정의한다.

```python
"""
    Algos module consists of all the basic algorithms and their implementation
"""

from __future__ import print

__all__ = ['searching', 'sorting']
__version__ = '0.0.1'
__author__ = 'Chitrank Dixit'

import os
import sys
```

[이 문서](https://www.python.org/dev/peps/pep-0257/)는 docstring를 작성하는 규칙을 설명한다.

<a name="naming"></a>

### 명명 규칙 (Naming Conventions)

Python으로 프로그램을 할 때 변수, 소스 코드와 문서에 있는 타입, 함수와 다른 엔터티들을 표기하는 식별자(identifier)로 사용하는 글자열(character sequence)를 만드는 규칙, 명명 규칙을 대부분 이용한다.

특별한 명명 스타일을 규정하지 않았다면 아래와 같이 기술한 것을 고려해 보자. - b 또는 소문자 한 글자 - B 또는 대문자 한 글자 - lowercase - UPPERCASE - lower*case_with_underscore - UPPER_CASE_WITH_UNDERSCORE - CapWords, CamelCase 또는 StudlyCaps로 알려진 CapitalizedWords - mixedCase - Capitalized_Words_With_Underscores - \_single\_leading\_underscore: 약한(weak) "내부 사용(internal use)" 지시자. 예를 들면, <code>from M import \*</code>는 밑줄 글자로 시작하는 이름의 객체는 import하지 않는다. - single\_trailing\_underscore*: <code> Tkinter.Toplevel(master, class*='ClassName')</code>처럼 Python 키워드(keyword)와 충돌을 피하기 위한 규칙으로 사용한다. - *\_double\_leading\_underscore: 클래스 애트리뷰트(attribute)를 명명할때, 이름 맹글링(mangling)을 한다 (클래스 <code>FooBar</code>, <code>\_\_boo</code>는 <code>\_FooBar\_\_boo</code>가 된다). - \_\_double\_leading\_and\_trailing\_underscore: 사용자가 관장하는 namespace에 존재하는 <code>\_\_init\_\_</code>, <code>\_\_import\_\_</code> 또는 <code>\_\_file\_\_</code>와 같은 "magic" 객체 또는 애트리뷰트. 이같은 이름은 사용하지 말아야 하며 오직 문서화에서만 사용하여야 한다.

#### 통산적인 명명 규칙 (General Naming Conventions)

아래 테이블은 식별자를 몀명하는 방법에 대한 통상적인 지침이다.

| 식별자          | 관례      |
|-----------------|-----------|
| 모듈            | lowercase |
| 클래스          | Capwords  |
| 함수            | lowercase |
| 메소드          | lowercase |
| 타입 변수       | CapWords  |
| 상수 (Constant) | UPPERCASE |
| 패키지          | lowercase |

-	한 글자 변수명에는 '1', 'O', 'l'은 사용하지 않는다. 이 글자들은 어떤 폰트에서 영(0)또는 (1)과 비슷하게 보이기 때문이다.
-	일반적으로 가능하다면 짧은 이름을 사용하는 것이 좋다. 어떤 경우에는 밑줄 글자 사용이 가독성을 향샹시키기도 한다.

<a name="compilant"></a>

### PEP-8 검증? (PEP-8 Compilant?)

PEP-8에 대하여 알고 난 다음에는 아마 작성한 코드가 지침 준수의 검증에 의문을 갖을 것이다 (그리고 아직 설명하지 못한 부분이 많다).

PEP-8에 대하여 알아보는 것에 앞서 간단한 <code>pep8</code> 모듈, <code>coala</code> 패키지 그리고 다음 절에서 소개할 다른 도구를 살펴 보아야 한다.

#### Python <code>pep8</code> 패키지

[pep8 패키지](https://pypi.python.org/pypi/pep8/1.7.1)는 코드의 PEP-8 준수 여부를 검사하며 PEP-8를 따를 수 있도록 수정을 제안한다.

<code>pip</code>를 이용하여 pep8을 설치한다.

```python
$ pip install pep8
```

예를 들면

```python
$ pep8 --first optparse.py
optparse.py:69:11: E401 multiple imports on one line
optparse.py:77:1: E302 expected 2 blank lines, found 1
optparse.py:88:5: E301 expected 1 blank line, found 0
optparse.py:222:34: W602 deprecated form of raising exception
optparse.py:347:31: E211 whitespace before '('
optparse.py:357:17: E201 whitespace after '{'
optparse.py:472:29: E221 multiple spaces before operator
optparse.py:544:21: W601 .has_key() is deprecated, use 'in'
```

<code>--show-source</code> 인수(argument)를 사용하여 준수하지 않은 소스 코드를 볼 수 있다.

```python
$ pep8 --show-source --show-pep8 testsuite/E40.py
testsuite/E40.py:2:10: E401 multiple imports on one line
import os, sys
         ^
    Imports should usually be on separate lines.

    Okay: import os\nimport sys
    E401: import sys, os
```

또는 <code>--statistics</code>를 사용하여 각 오류가 얼마나 발생하였는가를 볼 수 있다.

```python
$ pep8 --statistics -qq Python-2.5/Lib
232     E201 whitespace after '['
599     E202 whitespace before ')'
631     E203 whitespace before ','
842     E211 whitespace before '('
2531    E221 multiple spaces before operator
4473    E301 expected 1 blank line, found 0
4006    E302 expected 2 blank lines, found 1
165     E303 too many blank lines (4)
325     E401 multiple imports on one line
3615    E501 line too long (82 characters)
612     W601 .has_key() is deprecated, use 'in'
1188    W602 deprecated form of raising exception
```

[flake8](https://pypi.python.org/pypi/flake8), [autopep8](https://pypi.python.org/pypi/autopep8/) 또는 [pylint](https://pypi.python.org/pypi/pylint) 같은 다른 모듈도 살펴 보자.

#### <code>coala</code>를 이용한 코드 분석

여기에서는 Python 프로그래밍에 더 관심이 있을 지라도 <code>coala</code>는 모든 프로그래밍에 대하여 린팅(linting)과 수정을 지원한다. <code>pip</code>를 이용하여 <code>coala</code>를 설치할 수 있다.

```
$ pip3 install coala-bears
```

위에서 보인 것은 실제로 <code>coala-bears</code>를 설치한 것이다. <code>bears</code>는 <code>coala</code>를 확장한 프러그인(plugin) 또는 간단한 모듈로 프로그래밍 언어마다 다르다. 이 경우에는 <code>pep8bear</code>를 사용한다. 이는 PEP-8 미준수 코드를 찾아 해당 부분을 수정한다. Python 코드 검사에 사용을 고려하여야 한다.

```
$ coala -S python.bears=PEP8Bear python.files=\*\*/\*.py \
python.default_actions=PEP8Bear:ApplyPatchAction --save
# other output ...
Executing section python...
[INFO][11:03:37] Applied 'ApplyPatchAction' for 'PEP8Bear'.
[INFO][11:03:37] Applied 'ApplyPatchAction' for 'PEP8Bear'.
```

#### pep8online: 온라인으로 Python 코드 검사

간편한 <code>pep8</code> 모듈과 <code>coala</code> 패키지에 [pep8online](http://pep8online.com/)에서 작성한 Python 코드의 PEP-8 준수 여부를 검사할 수 있다. 이 사이트는 작성한 코드를 복사하여 "Check code" 버튼이 있는 편집기를 제공한다. 결과로 개선이 필요한 피드백을 보여준다. 매우 편리하다!

### 마치며

Python으로 프로그래밍 할때, 많은 사람들은 기능을 보다 빠르게 구현하고자 하는 생각에 코드 품질에 대하여는 등한시 한다. 그러나 이 문서에서 설명한 또는 아직 다루지 못한 내용들은 develop-staging-test-deploy 순환주기에 일부분이다. 이는 프로젝트에 참여하는 모든 개발자들이 이해할 수있는 이점이 있으며, 디버거를 이용하여 코드를 깊이 이해하지 않고도 코드를 수정하는 작업을 수행 할 수 있다. 오픈 소스 프로젝트에 참여하여 기여하려면, PEP-8가 편리하다는 것을 알게 될 것이고 보편적인 표준이기 때문에 코드를 더 잘 이해할 수 있을 것이다. 대부분의 파이썬 개발자는 이를 따른다.

이제 PEP-8에 대한 간단한 설명을 끝냈다. [PEP-8](https://www.python.org/dev/peps/pep-0008/)을 직접 확인해 보도록 하자. 보다 많은 것을 배울 수 있을 것이다.

이 문서는 Chitrank Dixit가 작성한 PEP-8 Tutorial: Code Standards in Python를 번역한 것이다.
