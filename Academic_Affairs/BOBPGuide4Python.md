Python "The Best of the Best Practices (BOBP)" 지침서
=====================================================

---

Python 프로그램 코딩을 위한 ["Best of the Best Practices" (BOBP)](https://gist.githubusercontent.com/sloria/7001839/raw/ccc38a965343929eaa83a3ea494b521f67b1d2e1/bobp-python.md) 지침서를 번역한 것입니다. Python 프로그램밍을 즐기시길 ...

In General
----------

---

### Values

-	"Build tools for others that you want to be built for you." - Kenneth Reitz
-	"Simplicity is alway better than functionality." - Pieter Hintjens
-	"Fit the 90% use-case. Ignore the nay sayers." - Kenneth Reitz
-	"Beautiful is better than ugly." - [PEP 20](http://www.python.org/dev/peps/pep-0020/)
-	공개 소프트웨어는 물론 비공개 소프트웨어 작성에서도.

### General Development Guidelines

-	"Explicit is better than implicit" - [PEP 20](http://www.python.org/dev/peps/pep-0020/)
-	"Readability counts." - [PEP 20](http://www.python.org/dev/peps/pep-0020/)
-	"Anybody can fix anything." - [Khan Academy Development Docs](https://sites.google.com/a/khanacademy.org/forge/for-developers)
-	[비효울적인 설계, 틀린 결정과 불량 코드](http://www.artima.com/intv/fixit2.html)는 *발견되는 즉시* 수정하십시요.
-	"Now is better than never." - [PEP 20](http://www.python.org/dev/peps/pep-0020/)
-	새로운 기능에 대하여 문서를 작성하고 테스트를 많이 하십시요.
-	Even more important that Test-Driven Development--*Human-Driven Development*
-	가이드라인은 변경될 수 있습니다.

In Particular
-------------

---

### Style

기본적으로 [PEP 8](PEP8Tutorial.md)를 준수합니다.

#### 명명 (Naming)

-	변수(variables), 함수(functions), 메소드(methods), 패키지(packages), 모듈(modules)
	-	<code>lower_case_with_underscores</code>
-	클래스(Classes)와 예외(Exceptions)
	-	<code>CapWords</code>
-	Protected 메소드와 내부 함수
	-	<code>\_single_leading_underscore(self, ...)</code>
-	Private 메소드
	-	<code>\__double_leading_underscore(self, ...)</code>
-	상수
	-	<code>ALL_CAPS_WITH_UNDERSCORES</code>

##### 일반적인 명명 규칙

매우 짧은 블록에서 의미가 즉각적인 문맥에서 명확하게 드러날 때를 제외하고는 <code>l</code>, <code>O</code>, <code>I</code>를 변수명에 사용하지 마십시요.

![yes](yes.png)

```Python
for e in elements:
    e.mutate()
```

레이블을 중복하여 사용하지 않습니다.

![no](no.png)

```Python
import audio

core = audio.AudioCore()
controller = audio.AudioController()
```

"역 표기(reverse notation)"를 사용하지 않습니다.

![yes](yes.png)

```Python
elements = ...
elements_active = ...
elements_defunct = ...
```

![no](no.png)

```Python
elements = ...
active_elements = ...
defunct_elements ...
```

getter와 setter 메소드를 사용하지 않습니다.

![yes](yes.png)

```Python
person.age = 42
```

![no](no.png)

```Python
person.set_age(42)
```

#### Indentation

이미 알고 있듯이 빈칸 4자를 사용합니다.

#### import

모듈 내의 개별 기호 대신 전체 모듈을 import 합니다. 예를 들면 상위 모듈 <code>canteen</code>이 <code>canteen/sessions.py</code> 파일을 포함한 경우라면,

![yes](yes.png)

```Python
import canteen
import canteen.sessions
from canteen import sessions
```

![no](no.png)

```Python
from canteen import get_user  # Symbol from canteen/__init__.py
from canteen.sessions import get_session  # Symbol from canteen/sessions.py
```

설명서에 명시적으로 개별 기호를 가져 오는 것으로 명시된 제 3 자가 작성한 코드의 경우는 예외적으로 허용할 수 있습니다.

이는 순환적인 import를 피하기 위한 것입니다. ([참조](https://sites.google.com/a/khanacademy.org/forge/for-developers/styleguide/python#TOC-Imports)\)

모든 import 문은 페이지 상단에 공백 라인으로 구분하여 세 부분으로 나누어 순서대로 작성합니다.

1.	표준 라이브러리 import문
2.	다른 커뮤니티에서 개발한 모듈/라이브러리 import문
3.	로컬 응용(application)/라이브러리 import문

이렇게 힘으로써 각 모듈의 출처를 분명히 할 수 있습니다.

#### 문서화 (Documentation)

[PEP 257](http://www.python.org/dev/peps/pep-0257/)의 docstring 지침을 따릅니다. 이 표준을 시행하는 데 [reStructured Text](http://docutils.sourceforge.net/docs/user/rst/quickref.html)와 [Sphinx](http://sphinx-doc.org/)가 도움을 줄 수 있습니다.

기능을 정확하게 설명하기 위해서는 한 줄의 docstring을 사용하십시오.

```Python
"""Return the pathname of ``foo``."""
```

한 줄이상의 docstring은 다음과 같아야 합니다.

-	요약
-	적절한 사용 예(Use case)
-	인수(Args)
-	반횐 값이 <code>None</code>이 아니면 반환 값의 데이터 타입과 의미

```Python
"""
Train a model to classify Foos and Bars.

Usage::

    >>> import klassify
    >>> data = [("green", "foo"), ("orange", "bar")]
    >>> classifier = klassify.train(data)

:param train_data: A list of tuples of the form ``(color, label)``.
:rtype: A :class:`Classifier <Classifier>`
"""
```

**Note** :

-	설명("Returns")하기 보다는 수행 단어 ("Return")를 사용합니다.
-	클래스의 docstring에서는 <code>\_\_init\_\_</code> 메소드를 설명합니다.

```python
class Person(object):
    """A simple representation of a human being.

    :param name: A string, the person's name.
    :param age: An int, the person's age.
    """
    def __init__(self, name, age):
        self.name = name
        self.age = age
```

##### 주석에서

많은 주석은 코드 가독성을 향샹시킵니다. 종종 조그만 메소드가 주석보다 효과적일 수 있습니다.

![no](no.png)

```Python
# If the sign is a stop sign
if sign.color == 'red' and sign.sides == 8:
    stop()
```

![yes](yes.png)

```python
def is_stop_sign(sign):
    return sign.color == 'red' and sign.sides == 8

if is_stop_sign(sign):
    stop()
```

#### 라인 길이 (Line Length)

80-100 자까지 사용할 수 있습니다. 신경을 너무 안쓰셔도 됩니다.

여러 줄을 사용하는 긴줄에서는 연속에 괄호를 사용합니다.

```python
 wiki = (
    "The Colt Python is a .357 Magnum caliber revolver formerly manufactured "
    "by Colt's Manufacturing Company of Hartford, Connecticut. It is sometimes "
    'referred to as a "Combat Magnum". It was first introduced in 1955, the '
    "same year as Smith & Wesson's M29 .44 Magnum."
)
```

### 테스팅

100 % 코드 커버리지를 위해 노력하지만 커버리지 스코어에 너무 집착하지 마십시오. (일정 수준이상이면 받아 드리십시요.)

#### 통상의 테스팅 지침

-	길고 설명적인 이름을 사용합니다. 이로 인하여 종종 테스트 메소드에서 docstring을 생략할 수 있습니다.
-	테스트를 격리하여야합니다. 특히 운영중인 데이터베이스 또는 네트워크와 상호 작용하지 않습니다. 일부분을 복사하거나 모의 객체를 사용하는 별도의 테스트 데이터베이스를 사용하십시오.
-	[공장](https://github.com/rbarrois/factory_boy)의 비품으로 취급하십시오.
-	불완전한 테스트를 절대 통과시키지 마십시오. 그렇지 않으면 잊어 버릴 위험이 있습니다. 대신 <code>assert False, "TODO : finish me"</code>와 같이 표시합니다.

#### 단위 테스트 (Unit Test)

-	작은 기능 하나에 집중합니다.
-	테스트를 빠르게 하십시오. 그러나 느리더라도 하지 않는 것보다 낫습니다.
-	단일 클래스 또는 모델에 대해 하나의 테스트 케이스 클래스를 갖는 것이 바람직합니다.

```Python
import unittest
import factories


class PersonTest(unittest.TestCase):
    def setUp(self):
        self.person = factories.PersonFactory()

    def test_has_age_in_dog_years(self):
        self.assertEqual(self.person.dog_years, self.person.age / 7)
```

#### 기능 테스트 (Functional Test)

기능 테스트는 최종 사용자가 응용프로그램과 상호 작용하는 방법에 가까운 상위 레벨 테스트입니다. 일반적으로 웹 및 GUI 응용 프로그램에서 사용합니다.

테스트를 시나리오로 작성하십시오. 테스트 케이스 및 테스트 메소드 이름은 시나리오 설명처럼 명명합니다. *테스트 코드를 작성하기 전에* 주석을 사용하여 스토리를 작성하십시오.

```Python
import unittest

class TestAUser(unittest.TestCase):

    def test_can_write_a_blog_post(self):
        # Goes to the her dashboard
        ...
        # Clicks "New Post"
        ...
        # Fills out the post form
        ...
        # Clicks "Submit"
        ...
        # Can see the new post
        ...
```

테스트 케이스와 테스트 메소드를 "Test A User can write a blog post"처럼 같이 함께 명명할 수 읽는 방법을 찾으십시오.

### 참고 문서

-	[PEP 20 (The Zen of Python)](http://www.python.org/dev/peps/pep-0020/)
-	[PEP 8 (Style Guide for Python)](PEP8Tutorial.md)
-	[The Hitchiker's Guide to Python](http://docs.python-guide.org/en/latest/)
-	Khan Academy Development Docs Python Best Practice Patterns Pythonic Sensibilities The Pragmatic Programmer
