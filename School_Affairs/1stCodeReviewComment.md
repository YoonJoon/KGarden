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

		import 문은 절대와 상대 import문으로 나눌 수 있습니다. Python에서는 가독성을 높이기 위하여 일반적으로 절대 import문을 선호한다. 프로그램이 복잡해 짐에 따라 상대 import문을 사용하기도 한다. 일반적으로 위의 "표준 라이브러리 import문"과 "다른 커뮤니티에서 개발한 모듈/라이브러리 import문"은 절대 import 문을 사용하며 "로컬 응용(application)/라이브러리 import문"은 상대 import문을 사용합니다. 따라서 아래와 같이 수정하여야 합니다.

		```Python
		...
		import json


		from django.shortcuts import render
		from django.http import JsonResponse
		from django.db import transaction
		from django.db.models import Q


		from ..utils import get_common_code
		from ..models import HighSchoolCode
		from ..hs01_high_school_code_u_forms import SearchHighSchoolCodeForm
		from ..utils import set_save_default_data
		...
		```

4.	[Python Naming Convention](PEP8Tutorial.md/#naming) 을 따라야 합니다.

5.	학적(School Register)서비스에서 사용하는 constant와 error code는 각각 school_register_constants.py와 school_register_error_codes.py로 만들어 주십시요.

	```Python
	\#!/usr/bin/env python
	\# encoding: utf-8
	"""
	school_register_constants.py
	"""


	...
	SEARCH_FORM = 'search_form'
	...
	REGION_CODE_ATTRIBUTE = "CS005"
	...


	```

	```Python
	\#!/usr/bin/env python
	\# encoding: utf-8
	"""
	school_register_error_codes.py
	"""


	...
	EX_EXCEPTION = "101"
	...


	```

	```Python
	\#!/usr/bin/env python
	\# encoding: utf-8
	"""
	hs01_high_school_code_u_views.py
	"""


	import ..school_register_constants
	import ..school_register_error_codes


	...


	try:
	    context = {
	        SEARCH_FORM: SearchHighSchoolCodeForm,
	            }
	    return render(request,
	                  'common/hs01hs01_high_school_code_u.html',
	                   context)
	except Exception as EX_EXCEPTION: print(ex)


	...


	try:
	    region_code = get_common_code(REGION_CODE_ATTRIBUTE)
	    data['region_code']=list(region_code)
	...


	```

6.	가급적 각 문장의 의미도 적어 주시면 고맙겠습니다.

	```Python
	    """
	    학기, 과정구분, 학생구분, 학적상태 콤보 데이터 가져오기
	    """


	    def hs01_high_school_code_u_search_combo(request): # 함수 정의 (?)
	      data = {} # 초기화
	      try:
	          region_code = get_common_code("REGION_CODE_ATTRIBUTE)  # 공통코드 테이블에서 지역코드 가져오기
	          data['region_code']=list(region_code)  # 지역코드 값 집합
	      except Exception as ex:  # 오류값 지정
	          data['msg'] = format(ex)
	      finally:
	          return JsonResponse(data, safe=False)
	```

7.	directory 구조를 어떻게 하는 것이 좋을지 같이 의논하여 봅시다.
