서버사이드 웹 프레임워크
------------------------

이 문서는 저작자 동의없이 KAIST 대학정보화사업팀을 위하여 [Server-side web framework](https://developer.mozilla.org/en-US/docs/Learn/Server-side/First_steps/Web_frameworks)를 번역 편집하여 작성한 것입니다.

이전에 웹 클라이언트와 서버 간의 통신 모습, HTTP 요청 및 응답의 특성, 웹 브라우저의 요청에 응답하기 위해 서버사이드 웹 응용프로그램이 수행해야 하는 것을 보여주었습니다. 이러한 지식을 바탕으로 웹 프레임워크가 서버사이드 웹 응용프로그램이 수행해야 하는 것들을 단순화하는 방법을 찾아 보고 처음 개발하는 사이트를 위한 서버사이드 웹 응용프로그램을 위한 프레임워크를 선택하는 방법에 대하여 알아 봅니다.

> 선수지식: 기본적인 컴퓨터 활용 능력과 서버사이드 코드가 HTTP 요청을 처리하고 응답하는 방법에 대한 기본적인 이해([클라이언트-서버 개요](clientServerOverview.md) 참조)가 필요합니다.
>
> 목표: 웹 프레임워크가 서버사이드 코드의 개발/유지 보수를 단순화하는 방법을 보이며, 개발자가 자신만의 독자적인 개발을 위한 프레임워크 선택의 고려사항을 제시합니다.

다음 절에서는 실제 웹 프레임워크에서 사용되는 코드 조각을 사용하여 몇 가지 사항을 설명합니다. 프레임워크의 특정 모듈 코드에 대하여 설명하므로 전부 이해하지 못하더라도 너무 걱정하지 마십시요.

### 개요

서버사이드 웹 프레임워크 ("웹 응용 프로그램 프레임워크"라고도 함)는 웹 응용프로그램을 작성하고 유지 관리하며 확장하는 소프트웨어 프레임워크입니다. 이는 적절한 핸들러로 URL 라우팅, 데이터베이스와의 상호 작용, 세션 및 사용자 권한 지원, 출력 형식 (예 : HTML, JSON, XML) 및 웹 공격에 대한 보안 향상과 같은 일반적인 웹 개발 작업을 단순화하는 도구 및 라이브러리를 제공합니다. 다음 섹션에서는 웹 프레임워크가 웹 애플리케이션 개발을 어떻게 쉽게 할 수 있는 지에 대해 자세히 설명합니다. 그런 다음 웹 프레임워크를 선택하는 데 사용할 수 있는 몇 가지 기준을 설명하고 몇 가지 옵션을 나열합니다.

### 웹 프레임워크 기능

웹 프레임워크는 도구 및 라이브러리를 제공하여 일반적인 웹 개발 작업을 단순화합니다. 서버사이드 웹 프레임워크를 사용할 필요는 없지만, 개발을 훨씬 편하므로 사용을 강력히 권고합니다.

이 절에서는 웹 프레임워크가 제공하는 기능 중 일부(모든 프레임워크가 이러한 모든 기능을 제공하지는 않음)를 설명합니다.

#### HTTP 요청과 응답에 대한 직접적인 처리

마지막 단원에서 보았듯이 웹 서버와 브라우저는 HTTP 프로토콜을 통해 통신합니다. 서버는 브라우저로 부터 HTTP 요청을 기다리고 HTTP 응답으로 정보를 반환합니다. 웹 프레임워크를 사용하면 간단한 구문을 작성하여 이러한 요청과 응답을 처리하기 위한 서버사이드 코드를 생성할 수 있습니다. 즉, 낮은 수준의 네트워킹 기본 요소가 아니라 쉽고 높은 수준의 코드와 상호 작용 하여 보다 쉽게 작업할 수 있습니다.

아래 예는 Django (Python) 웹 프레임워크에서 이것이 어떻게 작동하는 지 보여 줍니다. 모든 "view" 함수 (요청 처리기)는 요청 정보가 들어있는 HttpRequest 객체를 받고 포맷된 출력(이 경우에는 문자열)을 가진 HttpResponse 객체를 반환해야 합니다.

```Python
# Django view function
from django.http import HttpResponse

def index(request):
    # Get an HttpRequest (request)
    # perform operations using information from the request.
    # Return HttpResponse
    return HttpResponse('Output string to return')
```

#### 해당 핸들러에게 요청 전송

대부분 사이트는 다른 URL을 통해 접근할 수있는 다양한 리소스를 제공합니다. 이러한 모든 기능을 하나의 기능으로 처리하도록 유지하는 것이 쉽지 않으므로 웹 프레임워크는 URL 패턴을 특정 핸들러 함수에 매핑하는 간단한 메커니즘을 제공합니다. 이 방법은 기본 코드를 변경하지 않고도 특정 기능을 제공하는 데 사용되는 URL을 변경할 수 있기 때문에 유지 관리 측면에서 이점이 있습니다.

다른 프레임워크는 매핑을 위하여 다른 메커니즘을 사용합니다. 예를 들어 Flask (Python) 웹 프레임워크는 데코레이터를 사용하여 뷰 함수에 대한 경로를 추가합니다.

```Python
@app.route("/")
def hello():
    return "Hello World!"
```

Django에서는 개발자가 URL 패턴과 뷰 함수 사이에 URL 매핑 목록을 정의해야 합니다.

```Python
urlpatterns = [
    url(r'^$', views.index),
    # example: /best/myteamname/5/
    url(r'^(?P<team_name>\w.+?)/(?P<team_number>[0-9]+)/$', views.best),
]
```

#### 요청 데이터의 용이한 접근

HTTP 요청은 다양한 방법으로 데이터를 인코딩할 수 있습니다. 서버에서 파일 또는 데이터를 가져 오는 HTTP <code>GET</code> 요청은 URL 매개변수 또는 URL 구조에서 필요한 데이터를 인코딩 할 수 있습니다. 서버의 리소스를 업데이트하기 위한 HTTP <code>POST</code> 요청은 대신 요청 본문에 "POST data"로 업데이트 정보를 포함합니다. HTTP 요청은 클라이언트사이드 쿠키에 현재 세션 또는 사용자에 대한 정보를 포함할 수도 있습니다.

웹 프레임워크는이 정보에 접근하기 위한 프로그래밍 언어에 적합한 메커니즘을 제공합니다. 예를 들어 Django가 모든 view 함수에 전달하는 <code>HttpRequest></code> 객체는 대상 URL, 요청 유형 (예 : HTTP code>GET</code>), code>GET</code> 또는 <code>POST</code> 매개변수, 쿠키, 세션 데이터 등을 접근하기 위한 메서드와 속성을 포함합니다. Django는 또한 URL 매퍼에서 "캡처 패턴"을 정의하여 URL 구조로 인코딩된 정보를 전달합니다. (윗 절의 마지막 코드 참조)

#### 데이터베이스 접근의 추상화와 간편화

웹 사이트는 데이터베이스를 사용하여 사용자와 공유할 정보와 사용자에 대한 정보를 저장합니다. 웹 프레임워크는 종종 데이터베이스에 읽기, 쓰기, 쿼리 및 삭제 작업을 추상화하는 데이터베이스 계층을 제공합니다. 이 추상화 계층을 ORM(Object-Relational Mapper)이라고 합니다.

ORM을 사용하면 다음과 같은 두 가지 이점이 있습니다.

-	사용 중인 데이터베이스를 접근하는 코드 수정 없이도 데이터베이스를 변경할 수 있습니다. 이를 통해 개발자는 사용법에 따라 다른 데이터베이스들의 특성을 최적화할 수 있습니다.
-	데이터의 기본적인 유효성 검사를 프레임워크에 구현할 수 있습니다. 데이터를 데이터베이스 필드에 적절한 타입과 포맷(예: 전자 메일 주소)으로 저장하며, 어떤 방식으로든 요청의 부적절 여부 확인이 편리하고 안전합니다 (크래커는 특정 패턴의 코드를 사용하여 데이터베이스 레코드 삭제 등 악의적인 행위를 할 수 있습니다).

예를 들어 Django 웹 프레임워크는 ORM을 제공하며, 모델로 레코드 구조를 정의하여 사용하는 객체를 참조합니다. 모델은 저장될 필드 타입을 지정하고, 정보의 저장 가능 여부를 판단하는 필드 레벨 유효성 검사를 제공 할 수 있습니다 (예 : 이메일 필드는 유효한 이메일 주소만 허용). 또한, 최대 크기, 기본값, 선택 목록 옵션, 문서의 도움말 텍스트, 양식의 레이블 텍스트 등을 필드 정의에 지정할 수 있습니다. 모델은 코드와는 별도로 변경할 수 있는 구성에 대한 설정이기 때문에 접근하는 데이터베이스에 대한 어떠한 정보도 갖고 있지 않습니다.

아래 첫 코드 스니펫은 Team 객체에 대한 매우 간단한 Django 모델을 보여줍니다. 이는 팀 이름과 팀 레벨을 문자 필드로 저장하고 각 레코드에 저장할 최대 길이를 지정합니다. <code>team_level</code>은 값을 선택하는 필드이므로 기본값과 함께 표시할 선택 항목과 저장할 데이터 사이의 매핑을 제공합니다.

```Python
#best/models.py

from django.db import models

class Team(models.Model):
    team_name = models.CharField(max_length=40)

    TEAM_LEVELS = (
        ('U09', 'Under 09s'),
        ('U10', 'Under 10s'),
        ('U11, 'Under 11s'),
        ...  #list our other teams
    )
    team_level = models.CharField(max_length=3,choices=TEAM_LEVELS,default='U11')
```

Django 모델은 데이터베이스 검색을 위한 간단한 쿼리 API를 제공합니다. 이것은 서로 다른 조건(예 : 일치, 대소 문자를 구별, 크다 등)을 사용하여 한 번에 여러 필드와 비교할 수 있으며 복잡한 명령문을 지원할 수 있습니다 (예 : 팀이름이 "Fr"로 시작하거나 "al"로 끝나는 U11 팀에서 검색할 수 있습니다).

두 번째 코드 스니펫은 U09 팀을 모두 보여 주는 view 함수(리소스 핸들러) 입니다. 이 경우 <code>team_level</code> 필드가 정확히 'U09'인 모든 레코드를 필터링하려고 합니다 (이 조건을 필드 이름과 두 개의 밑줄로 표시한 <code><b>`team_level__exact`</b></code>의 일치 유형을 인수로 <code>filter()</code> 함수에 전달하는 방법에 유의하십시오).

```Python
#best/views.py

from django.shortcuts import render
from .models import Team

def youngest(request):
    list_teams = Team.objects.filter(team_level__exact="U09")
    context = {'youngest_teams': list_teams}
    return render(request, 'best/index.html', context)
```

#### 데이터 렌더링

웹 프레임워크는 종종 템플릿 시스템을 제공합니다. 이를 통해 페이지를 생성할 때 추가될 데이터의 표시 위치를 사용하여 출력 문서 구조를 지정할 수 있습니다. 템플리트는 종종 HTML을 생성하는 데 사용되지만 다른 유형의 문서를 작성할 수도 있습니다.

웹 프레임워크는 때때로 저장된 데이터를 JSON, XML 등과 같은 다른 형식으로 쉽게 생성 할 수있는 메커니즘을 제공합니다.

예를 들어 Django 템플릿 시스템을 사용하면 페이지가 렌더링될 때 view 함수에서 전달된 값으로 대체될 "double handlebars" 문법(예: <code>{ {variable_name} }</code>)을 사용하여 변수를 지정할 수 있습니다. 템플릿 시스템은 템플릿에 전달하는 반복 리스트 값과 같은 간단한 작업을 템플릿이 수행할 수있게 해주는 표현 (<code>{% expression %}</code> 문법)을 지원합니다.

> **note** : 다른 많은 템플리트 시스템은 Jinja2 (Python), handlebars (JavaScript), moustache (JavaScript) 등과 같은 다른 많은 템플리트 시스템에서도 유사한 문법을 사용합니다.

아래 코드 스니펫은 템플릿 수행을 보입니다. 이전 섹션의 "youngest 팀" 예제를 계속하면 뷰는 <code>youngest_teams</code>라는 리스트 변수를 HTML 템플리트로 전달합니다. HTML 뼈대 안에 <code>youngest_teams</code> 변수가 있는지 먼저 확인하고 다음 <code>for</code> 루프를 반복하는 표현식이 있습니다. 템플릿을 반복할 때마다 리스트에 있는 팀의 <code>team_name</code> 값을 보여 줍니다.

```html
#best/templates/best/index.html

<!DOCTYPE html>
<html lang="en">
<body>

 {% if youngest_teams %}
    <ul>
    {% for team in youngest_teams %}
        <li>{{ team.team_name }}</li>
    {% endfor %}
    </ul>
{% else %}
    <p>No teams are available.</p>
{% endif %}

</body>
</html>
```

### 웹 프레임워크 선택

사용하려는 거의 모든 프로그래밍 언어에 대해 수많은 웹 프레임워크가 존재합니다 (다음 섹션에서 몇 가지 인기있는 프레임워크를 나열합니다). 선택의 폭이 넓기 때문에 새로운 웹 애플리케이션을 위한 최선의 출발점을 제공하는 프레임워크를 찾기가 어려울 수 있습니다.

결정에 참고할 수 있는 요인은 다음과 같습니다.

-	**학습 노력**: 웹 프레임워크를 배우려는 노력은 사용 프로그래밍 언어, API의 일관성, 문서의 품질, 커뮤니티의 규모 및 활동에 얼마나 익숙한 지에 달려 있습니다. 프로그래밍 경험이 전혀 없다면 Django를 고려해보십시오 (위의 기준으로 가장 쉽게 배울 수 있습니다). 특정 웹 프레임워크 또는 프로그래밍 언어에 대해 이미 상당한 경험이 있는 개발 팀원이라면 사용하는 것을 따르는 것이 타당합니다.
-	**생산성**: 생산성은 프레임워크에 익숙해지면 얼마나 빨리 새 기능을 만들 수 있는지 측정하며 코드를 작성하고 유지 관리하기 위한 노력 (이전 기능은 손상된 상태에서 새 기능을 쓸 수 없기 때문에)을 포함합니다. 생산성에 영향을 미치는 많은 요소 문서화, 커뮤니티, 프로그래밍 경험 등은 "학습 노력"과 유사합니다.
	-	<i>프레임워크 목적/출처</i>: 일부 웹 프레임워크는 처음에는 특정 유형의 문제를 해결하기 위해 만들어졌으므로 비슷한 제약 조건의 웹 응용프로그램을 만들 때 더 좋습니다. 예를 들어, Django는 신문 웹 사이트의 개발을 지원하기 위해 만들어 졌으므로 블로그 및 기타 게시 사이트에 유용합니다. 반대로 Flask는 훨씬 가벼운 프레임워크이며 임베디드 장치에서 실행되는 웹 응용프로그램을 만드는 데 적합합니다.
	-	<i>분명함 대 불분명</i>: 독창적인 프레임워크는 특정 문제를 해결하기 위해 권장되는 "최선의" 방법을 지원하는 프레임워크입니다. 의견이 분명한 프레임워크로 공통 문제를 해결하려고 할 때 바른 방향으로 인도하기 때문에 더 생산적일 수 있지만 때로는 유연성이 떨어질 수 있습니다.
	-	<i>건전지 포함(battery included) 대 스스로 얻기</i>: 일부 웹 프레임워크에는 개발자가 "기본적으로" 생각할 수있는 모든 문제를 해결하는 도구/라이브러리를 포함하고 있습니다. 반면 경량 프레임워크는 웹 개발자가 개별 라이브러리의 문제에 대한 해결책을 선택하고 채택합니다 (장고는 전자의 예이며, Flask는 매우 가벼운 프레임워크의 예입니다). 모든 것을 포함하는 프레임워크는 이미 필요한 모든 것을 갖추었고 통합과 문서화가 잘 되었을 가능성이 크므로 시작하기가 쉽습니다. 그러나 작은 프레임워크에 필요한 모든 것이 있다면 제약이 많은 환경에서 실행할 수 있습니다. 또한, 작고 익히기 쉬운 것으로 구성할 수 있습니다.
	-	<i>프레임워크가 바람직한 개발 관행을 장려하는지 여부</i>: 예를 들어, [Model-View-Controller](https://developer.mozilla.org/en-US/docs/Web/Apps/Fundamentals/Modern_web_app_architecture/MVC_architecture) 아키텍처로 코드를 논리적 함수로 분리하도록 권장하는 프레임워크는 개발자가 작성한 어떤 코드보다 유지 관리가 용이한 코드를 얻을 수 있습니다. 유사하게 프레임워크 디자인은 코드의 테스트와 재사용을 용이하도록 하는 것에 큰 영향을 미칠 수 있습니다.
-	**프레임워크/프로그래밍 언어의 성능**: 보통 하드웨어에서 실행되는 중간 규모 사이트의 경우 Python과 같은 비교적 느린 런타임으로도 "충분 함" 이상의 성능을 보이므로 일반적으로 "속도"는 선택의 가장 큰 요소가 아닙니다. C ++ 또는 JavaScript같은 다른 언어의 인지된 속도 이점을 학습 및 유지 관리 비용으로 상쇄할 수 있습니다.
-	**캐싱 지원**: 웹 사이트가 더 성공적으로 접어 들면 사용자가 접근으로 더 많은 요청을 처리 할 수 없습니다. 이 시점에서 캐싱에 대한 지원을 추가로 고려할 수 있습니다. 캐싱은 이후 요청에서 다시 계산할 필요가 없도록 웹 요청의 전부 또는 일부를 저장하는 최적화입니다. 캐시된 요청을 반환하는 것은 처음부터 계산하는 것보다 훨씬 빠릅니다. 캐싱은 코드 또는 서버에서 구현할 수 있습니다 ([역방향 프록시](https://en.wikipedia.org/wiki/Reverse_proxy) 참조). 웹 프레임워크는 다양한 수준에서 캐시 가능한 컨텐츠를 정의할 수 있도록 지원합니다.
-	**확장성**: 웹 사이트가 환상적으로 성공하면 캐싱의 이점을 소진하고 더 강력한 하드웨어에서 웹 응용프로그램을 실행하는 수직 확장의 한계에 도달합니다. 이 시점에서 일부 고객은 서버에서 멀어지기 때문에 수평적으로 확장(여러 웹 서버 및 데이터베이스를 사이트에 배포하여 부하를 분산)하거나 "지리적으로" 확장하여야 합니다. 선택한 웹 프레임워크가 사이트를 얼마나 쉽게 확장 할 수 있는 지에 따라 큰 차이가 날 수 있습니다.
-	**웹 보안**: 일부 웹 프레임워크는 일반적인 웹 공격을 처리하는 데 더 나은 지원을 제공합니다. 장고를 예를 들면 HTML 템플리트에서 모든 사용자 입력을 삭제하므로 사용자가 입력 한 JavaScript를 실행할 수 없습니다. 다른 프레임워크도 비슷한 보호 기능을 제공하지만 기본적으로 항상 활성화되어 있지 않습니다.

프레임워크가 활발히 개발되고 있는지 여부는 라이센싱을 포함하여 많은 다른 가능한 요인이 있습니다.

프로그래밍 초보자라면 "학습 용이성"에 따라 프레임워크를 선택하게 될 것입니다. 언어 자체의 "사용 편의성"외에도 고품질의 문서/튜토리얼 및 새로운 사용자를 돕는 적극적인 커뮤니티가 가장 귀중한 리소스입니다. 배우기 쉽고 좋은 지원을 받을 수 있으므로 [Django](https://www.djangoproject.com/) (Python)와 [Express](http://expressjs.com/)(Node/JavaScript)를 선택하여 뒤에 나오는 예제를 작성할 것 입니다.

> **note** : [Django](https://www.djangoproject.com/) (Python)와 [Express](http://expressjs.com/)(Node/JavaScript)의 메인 웹 사이트에서 문서와 커뮤니티를 확인하십시오.
>
> 1.	(위 링크의) 메인 사이트로 이동하여
>
> 	-	( "Documentation, Guide, API Reference, Getting Started"와 같은 이름들의) Documentation 메뉴 링크를 클릭하십시오.
> 	-	URL 라우팅, 템플릿과 데이터베이스 / 모델을 설정하는 방법을 보여주는 항목을 볼 수 있습니까?
> 	-	문서가 명확합니까?
>
> 2.	각 사이트의 (커뮤니티 링크에서 접근 가능한) 메일링 리스트로 이동하여
>
> 	-	지난 며칠 동안 몇 개의 질문이 게시 되었습니까?
> 	-	얼마나 많은 응답이 있습니까?
> 	-	적극적인 공동체를 가지고 있습니까?
>

### 추천하는 프레임워크

이제 몇몇 서버사이드 웹 프레임워크를 살펴 보겠습니다.

아래의 서버사이드 프레임워크는 작성 당시 가장 많이 사용되는 프레임워크 중 일부입니다. 그들 모두는 생산성을 위해 필요한 모든 것을 갖추고 있습니다. 오픈 소스이며, 활발한 개발 활동을 펼치고 있으며, 문서를 작성하고 토론 게시판에서 사용자를 돕는 많은 열광적인 공동체가 있으며 유명 웹 사이트에서 사용되고 있는 것입니다. 기본적인 인터넷 검색으로 다른 많은 훌륭한 서버사이드 프레임워크를 발견할 수 있습니다.

> **note** : 프레임워크 웹 사이트에서 (부분적으로) 인용하여 설명하였습니다.

#### Django (Python)

[Django](https://www.djangoproject.com/)는 신속한 개발과 깨끗하고 실용적인 디자인을 장려하는 고급 Python 웹 프레임워크입니다. 숙련된 개발자가 제작하여 웹 개발의 번거로움을 덜어 주므로 바퀴를 다시 만들 필요없이 앱을 작성하는 데 집중할 수 있습니다. 무료이며 오픈 소스입니다.

Django는 "건전지 포함" 철학을 따르며 대부분의 개발자가 "즉시"할 수있는 모든 것을 제공합니다. 모든 것이 포함되기 때문에 모든 것이 함께 작동하고 일관된 디자인 원칙을 따르며 광범위한 최신 문서가 있습니다. 또한 빠르고 안전하며 확장성이 뛰어납니다. 파이썬을 기반으로하기 때문에 Django 코드는 읽기 쉽고 유지하기 쉽습니다.

Django를 사용하는 인기있는 사이트로는 Django 홈페이지부터 시작하여Disqus, Instagram, Knight Foundation, MacArthur Foundation, Mozilla, 내셔널 지오그래픽, Open Knowledge Foundation, Pinterest, Open Stack 등이 있습니다.

#### Flask (Python)

[Flask](http://flask.pocoo.org/)는 파이썬을 위한 마이크로 프레임워크입니다.

미니멀리즘하면서 플라스크는 진지한 웹 사이트를 만들 수 있습니다. 개발 서버 및 디버거를 포함하며 [inja2](https://github.com/pallets/jinja) 템플릿 작성, 보안 쿠키, [유닛 테스트](https://en.wikipedia.org/wiki/Unit_testing) 및 [RESTful](http://www.restapitutorial.com/lessons/restfulresourcenaming.html) 요청 전달을 지원합니다. 좋은 문서와 활발한 커뮤니티가 있습니다.

플라스크는 특히 리소스가 제한적인 소규모 시스템 (예 : 라즈베리 파이, 드론 컨트롤러 등의 웹 서버 실행)에서 웹 서비스를 제공해야 하는 개발자들에게 매우 인기가 있습니다.

#### Express (Node.js/JavaScript)

[Express](http://expressjs.com/)는 [Node.js](https://nodejs.org/en/)를 위한 신속하고 적응력이 뛰어나고 유연하며 미니멀 한 웹 프레임워크입니다 (노드는 JavaScript를 실행하기위한 브라우저 없는 환경입니다). 웹 및 모바일 애플리케이션을 위한 강력한 기능 세트를 제공하고 유용한 HTTP 유틸리티 메소드와 [미들웨어](https://developer.mozilla.org/en-US/docs/Glossary/Middleware)를 제공합니다.

부분적으로 클라이언트사이드 JavaScript 웹 프로그래머의 서버사이드 개발로 마이그레이션이 용이하고 부분적으로 자원 효율적이기 때문에 Express를 많이 사용합니다 (기본 노드 환경에서 모든 새로운 웹 요청에 대하여 별도의 프로세스를 생성하지 않고 스레드에서 경량 멀티 태스킹을 합니다. ).

Express는 최소의 웹 프레임워크이므로 사용하고자 하는 모든 구성 요소를 통합하지 않습니다 (예를 들면, 독립 라이브러리를 통해 데이터베이스 접근과 사용자 및 세션 지원을 제공합니다). 우수한 독립 요소가 많이 있지만 때로는 특정 목적을 위해 최선의 방법을 찾기가 어려울 수 있습니다.

[Feathers](http://feathersjs.com/), [ItemsAPI](https://www.itemsapi.com/), [KeystoneJS](http://keystonejs.com/), [Kraken](http://krakenjs.com/), [LoopBack](http://loopback.io/), [MEAN](http://mean.io/) 및 [Sails](http://sailsjs.org/)는 Express 기반의 인기있는 서버사이드 및 (서버 및 클라이언트사이드 프레임워크 함께 구성된) 풀 스택 프레임워크입니다.

Uber, Accenture, IBM 등 많은 유명 회사가 Express를 사용합니다 (목록은 [여기](http://expressjs.com/en/resources/companies-using-express.html)에).

#### Ruby on Rails (Ruby)

[Rails](http://rubyonrails.org/)(일반적으로 "Ruby on Rails"라고 함)는 Ruby 프로그래밍 언어로 작성된 웹 프레임워크입니다.

Rails는 Django와 매우 비슷한 디자인 철학을 따릅니다. Django와 마찬가지로 URL 라우팅, 데이터베이스에 데이터 접근, 템플릿에서 HTML 생성, JSON 또는 XML 형식의 데이터 형식 지정을 위한 표준 메커니즘을 제공합니다. DRY ( "dont repeat yourself"- 가능하다면 코드를 한 번만 쓰는 것), MVC (model-view-controller) 및 기타 여러 가지 디자인 패턴의 사용을 유사하게 권장합니다.

특정 디자인 결정 및 언어의 특성으로 인해 물론 많은 차이가 있습니다.

Rails는 [Basecamp](https://basecamp.com/), [GitHub](https://github.com/), [Shopify](https://shopify.com/), [Airbnb](https://airbnb.com/), [Twitch](https://twitch.tv/), [SoundCloud](https://soundcloud.com/), [Hulu](https://hulu.com/), [Zendesk](https://zendesk.com/), [Square](https://square.com/), [Highrise](https://highrisehq.com/) 등 유명 사이트에 사용되었습니다.

#### Laravel (PHP)

[Laravel](https://laravel.com/)은 표현력이 풍부하고 우아한 문법을 사용하는 웹 애플리케이션 프레임워크입니다. Laravel은 대부분의 웹 프로젝트에서 일반적으로 사용되는 다음과 같은 작업을 줄임으로써 개발의 어려움을 줄이려고 시도합니다.

-	[간단하고 빠른 라우팅 엔진](https://laravel.com/docs/routing).
-	[강력한 의존성 주입 컨테이너](https://laravel.com/docs/container).
-	[세션](https://laravel.com/docs/session)과 [캐시](https://laravel.com/docs/cache) 저장을 위한 다중 백엔드.
-	표현력이 풍부하고 직관적인 [데이터베이스 ORM](https://laravel.com/docs/eloquent).
-	데이터베이스에 독립적인 [스키마 마이그레이션](https://laravel.com/docs/migrations)
-	[견고한 백그라운드 작업 처리](https://laravel.com/docs/queues).
-	[실시간 이벤트 브로드캐스팅](https://laravel.com/docs/broadcasting).

Laravel은 액세스 가능하면서도 강력하여 크고 견고한 응용 프로그램 개발에 필요한 도구를 제공합니다.

#### ASP.NET

ASP.NET은 현대식 웹 응용프로그램과 서비스를 구축하기 위해 Microsoft에서 개발한 오픈 소스 웹 프레임워크입니다. ASP.NET을 사용하면 HTML, CSS 및 JavaScript를 기반으로 웹 사이트를 신속하게 만들 수 있으며, 수백만 명의 사용자가 사용할 수 있도록 확장 가능하며, 웹 API, 데이터 양식 또는 실시간 통신과 같은 복잡한 기능을 쉽게 추가할 수 있습니다.

ASP.NET의 차별화 요소 중 하나는 [CLR(Common Language Runtime)](https://en.wikipedia.org/wiki/Common_Language_Runtime)을 기반으로 하므로 지원되는 .NET 언어 (C #, Visual Basic 등)를 사용하여 ASP.NET 코드를 작성할 수 있습니다. 많은 Microsoft 제품과 마찬가지로 우수한 도구 (무료 인 경우도 있음), 활발한 개발자 커뮤니티 및 잘 쓰여진 문서의 장점을 활용할 수 있습니다.

Microsoft, Xbox.com, Stack Overflow 등 기타 여러 곳에서 ASP.NET을 사용하고 있습니다.

#### Mojolicious (Perl)

[Mojolicious](http://mojolicious.org/)는 Perl 프로그래밍 언어를 위한 차세대 웹 프레임워크입니다.

웹 초기에 많은 사람들은 [CGI](https://metacpan.org/module/CGI)라는 멋진 Perl 라이브러리 때문에 Perl을 배웠습니다. 언어에 대해 잘 알지 못하더라도 개발을 시작할 수 있을 정도로 간단하였고, 계속하여 사용할 수 있을 만큼 강력하였습니다. Mojolicious는 최첨단 기술을 사용하여 이 아이디어를 구현합니다.

Mojolicious가 제공하는 기능 중 일부는 다음과 같습니다.

-	단일 파일 프로토타입을 구조화된 MVC 웹 응용프로그램으로 쉽게 확장 할 수 있는 **실시간 웹 프레임워크**.
-	RESTful 경로, 플러그인, 명령, Perl-ish 템플릿, 내용 협상, 세션 관리, 양식 유효성 검사, 프레임워크
-	테스트, 정적 파일 서버, CGI/PSGI 탐지 및 일급 유니 코드 지원
-	IPv6, TLS, SNI, IDNA, HTTP/SOCKS5 프록시, UNIX 도메인 소켓, Comet(긴 폴링), 연결 유지, 연결 풀링, 타임 아웃, 쿠키, 멀티 파트 및 gzip 압축 지원하는 풀 스택 HTTP와 WebSocket 클라이언트/서버 구현.
-	JSON와 HTML/XML 파서 및 CSS 선택기 생성기 지원.
-	공개된 깨끗하고 포터블한 객체 지향적인 순수한 Perl API.
-	다년간의 경험에 기반하는 신선한 코드 그리고 무료 및 오픈 소스.

#### Spring Boot (Java)

[Spring Boot](https://spring.io/projects/spring-boot)는 [Spring](http://spring.io/)에서 제공하는 많은 프로젝트 중 하나입니다. [Java](https://www.java.com/)를 사용하여 서버사이드 웹 개발을 수행하는 좋은 출발점입니다.

[Java](https://www.java.com/) 기반의 유일한 프레임워크는 아니지만 "실행"할 수있는 독립형 프로덕션급 Spring 기반 응용프로그램을 만드는 데 사용하기 쉽습니다. Spring 플랫폼 및 타사 라이브러리에 대한 의견이 분분하지만 최소한의 수선과 구성으로 시작할 수 있습니다.

작은 사이트에서도 사용할 수 있지만 강점은 클라우드 방식을 사용하는 대규모 응용프로그램을 구축하는 데 있습니다. 대개 여러 응용프로그램은 서로 대화하면서 병렬로 실행됩니다. 일부 응용프로그램은 사용자 상호 작용을 제공하고 다른 응용 프로그램은 백엔드 작업 (예 : 데이터베이스 접근 또는 다른 서비스 요청)을 수행합니다. 응답성을 보장하기 위하여 로드 밸런서는 중복과 신뢰성을 보장하거나 사용자 요청을 원격에서 처리합니다.

### Summary

웹 프레임워크가 서버사이드 코드를 보다 쉽게 개발하고 유지할 수 있음을 이 단계에서는 보여주었습니다. 또한 몇 가지 보편적인 프레임워크에 대한 개략적인 개요를 설명하였고 웹 응용프로그램 프레임워크를 선택하기 위한 기준을 논의했습니다. 이제는 자신의 서버사이드 개발을 위해 웹 프레임워크를 선택하는 방법에 대한 아이디어가 있어야합니다. 그렇지 않더라도 걱정할 필요가 없습니다. 나중에 우리는 Django와 Express에 대한 상세한 자습서를 제공하여 실제로 웹 프레임워크로 작업한 경험을 공유할 것입니다.

이 단원의 다음 단계는 방향을 약간 바꾸어 웹 보안을 다룰 것입니다.

### 이 단원에서 아래 단계를 다룹니다.

-	[서버사이드 소개](introServer.md)
-	[클라이언트-서버 개요](clientServerOverview.md)
-	[서버사이드 웹 프레임워크](serverSideWebFrameWork.md)
-	[웹사이트 보안](webSiteSecurity.md)
