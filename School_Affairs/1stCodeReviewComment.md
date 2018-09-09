### <code>common/hs01_high_school_code_u_views.py</code> 코드를 통하여 본 1st Common Code Review Comments

#### 공통 comments:

1.	일단 모든 프로그램 파일 (“모듈”이라 함)에 첫 문장은 copyright statements로 시작합니다. (우리 project에서는 repository(<code>01_Student_administratuve_Service</code>)에 한번만 선언하기로 하였으므 repository내의 모든 파일에서는 생략할 수 있습니다.)

2.	copyright statements 다음에는 이 모듈(파일)에 어떤 class와 function들을 정의하고 있으며 각 class와 function은 어떤 기능을 수행하는가 아래와 같이 간단히 기술합니다. (예: <code>common/hs01_high_school_code_u_views.py</code>\)

	```Python
	"""
	hs01_high_school_code_u : url 요청시 기본업무화면을 띄운다. hs01_high_school_code_u_search_combo : 학기, 과정구분, 학생구분, 학적상태 콤보 데이터 가져오기
	hs01_high_school_code_u_search : 조회
	hs01_high_school_code_u_save ; 신규 또는 수정 저장, transaction으로 처리 hs01_high_school_code_u_delete : 삭제, transaction으로 처리
	"""


	from django.shortcuts import render
	from django.http import JsonResponse
	from common.utils import get_common_code ...
	```

3.	import statements를 기술합니다([참조](PEP8Tutorial.md/#import)). (이때 모듈에 공통적인 것은 여기에 정의하고 한 function에서만 사용하는 것은 그 function에서 정의합니다. import statements는 다음 순서로 정의합니다.

	1.	표준 라이브러리 import문
	2.	다른 커뮤니티에서 개발한 모듈/라이브러리 import문
	3.	로컬 응용(application)/라이브러리 import문

4.	import 문에는
