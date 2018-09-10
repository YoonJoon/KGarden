SW 개발 프로세스
----------------

K-Garden, KAIST CRP(Campus Resource Planning System)의 Software Developemnt Process를 정의한 문서이다. User Requirements를 분석하여 RFP를 작성하고 외주 업체를 선정하여 개발을 시작하는 이후 프로세스를 기술한다.

1.	Created Mar. 19, 2018 by 이윤준

2.	Revised Sep. 10, 2018 by 이윤준

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

---

### K-Garden Service 와 Module 명과 영문명

#### Lilac

학사 서비스 시스템

영문: Academic_Affairs

-	학적 : Academic_Registra

#### Calla

연구 지원 서비스 시스템

영문: Research_Affairs

#### Lavender

일반 행정 서비스 시스템

영문: General_Affairs

-	인사 : Human_Resource_Management

#### Vervena

인프라 서비스 시스템

---

### Program Development Workflow

개발하는 SW 품질을 일정 수준 이상 유지하기 위하여 개발 단계에서 부터 다음에 기술한 단계를 거쳐 program을 개발하여야 합니다.

1.	Coding Style Check

	-	개발자는 Eclipse에 plugin되어 있는 [Sonarlint](https://www.sonarlint.org/eclipse/)를 사용하여 프로그램 style check 합니다.

	Python program의 coding style은 [PEP8: Python Style 지침서](Acdemic_affairs/PEP8Tutorial.md)와 [The Best of the Best Practices (BOBP) Guide for Python](https://gist.github.com/sloria/7001839)을 참고 하십시요.

2.	정적 분석 (Static Analysis)

	1.	위 단계를 거친 후 개발자는 코드를 develop 브랜치에 push합니다.
	2.	이후 [Jeckins](https://jenkins.io/)는 [SonarQube](https://www.sonarqube.org/)를 호출하여 정적분석을 수행합니다.
	3.	그 실행 결과로 Jenkins, SonarQube에 실행 결과 report를 게시하고 이를 Slack을 통하여 알립니다.

3.	단위 테스트 (Unit Test)와 Code Coverage

	[단위 테스트란 무엇인가? 왜 단위 테스트를 해야하는가?](https://cjh5414.github.io/why-pytest/)

	[How to properly use coverage.py in Python?](https://stackoverflow.com/questions/36517137/how-to-properly-use-coverage-py-in-python)

	1.	SonarQube를 이용하여 Static Analysis를 결과에 fatal error가 없으면, SonarQube는 [python unittest framework](https://docs.python.org/3/library/unittest.html)를 이용하여 unit test를 실행합니다.

	2.	SonarQube에서 test case의 실행 결과를 볼 수 있습니다. 이 또한 Slack을 통하여 알립니다.

	3.	이와 함께 SonarQube는 [Coverage.py](https://coverage.readthedocs.io/en/coverage-4.5.1a/)를 이용하여 unittest를 수행하여 얻은 code coverage를 출력합니다.
