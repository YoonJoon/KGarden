SW 개발 프로세스
----------------

K-Garden, KAIST CRP(Campus Resource Planning System)의 Software Developemnt Process를 정의한 문서이다. User Requirements를 분석하여 RFP를 작성하고 외주 업체를 선정하여 개발을 시작하는 이후 프로세스를 기술한다.

Created Mar. 19, 2018 by 이윤준

### 개발을 시작하기 전에 준비하여 개발자에게 제공해야 할 사항

-	개발 환경 set up 및 표준 확정

-	문서 작성

	-	내부 문서는 가급적 markdown 형식으로 작성하여 repository에 저장하며 버전 관리를 한다. 문서번호는 작성자+작성년월일+일년번호(2자리)로 구성한다 (예:윤준-20180321-01).
	-	[마크다운(markdown) 작성법](https://gist.github.com/ihoneymon/652be052a0727ad59601)
	-	마크다운 편집기 [Atom](https://atom.io/)
	-	[Atom 편집기 개요](https://opentutorials.org/module/1579)
	-	[markdown 문서 편집을 위한 Atom 설치 및 사용](https://innks.github.io/2017/04/23/IT/Atom-Editor/)
	-	[Atom 을 마크다운(Markdown) 에디터로 사용하기](https://www.portent.com/blog/content-strategy/atom-markdown.htm)

-	Version Management를 위하여 remote repository GitLab 사용

-	copyright 및 개발자 comment 예시 준비[Example on how to document your Python docstrings](https://thomas-cokelaer.info/tutorials/sphinx/docstring_python.html) 제시할 것

-	Qulaity Control을 SonarQube를 사용하여 code review, style check, static analysis, unit test를 수행하며 이 process gate measure로 code coverage를 사용한다.

-	IDE Eclipse (Pyhton, Java) code review, style check, static analysis, unit test에 필요한 plugin을 설치하여 사용한다.

-	Code Review

	-	code review는 외주 개발자 1인과 내부 개발자 1인이 수행하며 그 내용은 ??에 기술

### Service 와 Module 명과 영문명

#### Lilac Service System (학사서비스시스템)

-	학사 서비스 영문: School_Affairs

	-	학적 : Academic_Registra

---

-	[The Best of the Best Practices (BOBP) Guide for Python](https://gist.github.com/sloria/7001839)

-	Static Analysis & Coding Style Check

	-	개발자는 [Pylint](https://www.pylint.org/)를 사용하여 그 결과를 ??에 report

-	Unit Test & Code Coverage

	-	[How to properly use coverage.py in Python?](https://stackoverflow.com/questions/36517137/how-to-properly-use-coverage-py-in-python)
	-	[Coverage.py](http://coverage.readthedocs.io/en/latest/)
	-	[단위 테스트란 무엇인가? 왜 단위 테스트를 해야하는가? 왜 pytest를 사용해야 하는가?](https://cjh5414.github.io/why-pytest/)
	-	[Python 프로젝트에 Codecov 연동하기](https://cjh5414.github.io/codecov-python/)
