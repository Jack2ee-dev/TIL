# ARIA

> 이 글은 MDN의 ['An overview of accessible web applications and widgets'](https://developer.mozilla.org/ko/docs/Web/Accessibility/An_overview_of_accessible_web_applications_and_widgets)을 번역하고 정리한 글이다.

## 설명

**접근가능한 리치 인터넷 어플리케이션**(Accessible Rich Internet Applications, **ARIA**)은 장애를 가진 사용자가 웹 콘턴츠와 웹 어플리케이션(특히 JavaScript를 사용하여 개발할 경우)에 더 쉽게 접근할 수 있는 방법을 정의하는 여러 특성을 말한다.

ARIA는 HTML을 보충해, 일반적으로 보조 기술이 알 수 없는 상호작용 및 흔히 쓰이는 어플리케이션 위젯에 필요한 정보를 제공한다. 예를 들어 ARIA는 HTML4에서의 탐색 랜드마크, JavaScript 위젯, 폼 힌트 및 오류 메시지, 실시간 콘텐츠 업데이트 등을 접근 가능한 형태로 제공한다.

> ARIA는 HTML4를 보충할 목적으로 나왔다. ARIA의 많은 위젯은 HTML5로 통합되었으므로, semantic HTML을 ARIA보다 선호해야 한다.

예시) 진행 표시줄(Progress Bar)의 위젯 마크업의 예이다.

> ```html
<div 
    id="percent-loaded" 
    role="progressbar" 
    aria-valuenow="75" 
    aria-valuemin="0" 
    aria-valuemax="100"
>

</div>
```

ARIA는 W3C의 Web Accessbility Initiative에서 제작하고, 스크린리더 같은 보조기기에서 필요한 정보들을 추가하는 방법을 제공한다. ARIA는 마크업에서 특별한 속성을 추가하여 개발자들이 위젯의 디테일한 정보를 제공할 때 사용한다.
동적 웹 어플리케이션에서 찾을 수 있는 데스크탑 스타일 컨트롤과 표준 HTML 태그 사이에 있는 차이를 채우기 위해, ARIA는 친숙한 UI 위젯의 동작 상태(state)와 역할(Role)에 대한 설명을 제공한다.

ARIA는 다른 타입의 속성 **R**oles, **S**tates, **P**roperties(RSP)를 분할하여 정의한다. Roles는 slider, menu bar, dialog와 같은 HTML4에서 사용하지 못하는 위젯을 설명한다. Properties는 드래그가 가능하다는 것이나, 요소가 필요하다는 것이나, 팝업이 뜨는 것과 같은 위젯의 특징에 대해 설명한다.
State는 요소의 현재 상태에 대해 설명한다. 이 정보는 보조기기에서 요소의 접근이 불가하거나, 숨겨져 있는 상태라는 것을 명시한다.

ARIA 속성은 브라우저에 의해 운영체제의 접근성 API에 자동으로 해석되도록 디자인되었다. ARIA가 있을 때, 보조 기기는 데스크탑이 하는 방식과 마찬가지로 커스텀 자바스크립트 명령을 인식하고 상호작용할 수 있다.
이는 이전 세대의 웹 어플리케이션에서 가능했던 더 일관적인 사용성을 제공할 수 있다.

예시) ARIA 속성이 더해진 탭 위젯을 위한 마크업
```html
<ol role="tablist">
    <li id="ch1Tab" role="tab">
        <a href="#ch1Panel">Chapter 1</a>
    </li>
    <li id="ch2Tab" role="tab">
        <a href="#ch2Panel">Chapter 2</a>
    </li>
    <li id="quizTab" role="tab">
        <a href="#quizPanel">Quiz</a>
    </li>
</ol>

<div>
    <div id="ch1Panel" role="tabpanel" aria-labelledby="ch1Tab">Chapter 1 content goes here</div>
    <div id="ch2Panel" role="tabpanel" aria-labelledby="ch2Tab">Chapter 2 content goes here</div>
    <div id="quizPanel" role="tabpanel" aria-labelledby="quizTab">Quiz content goes here</div>
    
</div>
```

ARIA는 Firefox, Safari, Opera, Chrome 및 IE를 포함한 모든 주요 브라우저의 최신 번전에서 지원됩니다. 스크린 리더와 같은 많은 보조 기술도 ARIA를 지원한다.

## 대표적 변화

ARIA는 UI 위젯의 현재 상태 선언 속성을 제공한다.

- aria-checked: 체크박스 혹은 라디오 버튼의 상태를 표시한다.
- aria-disabled: 요소는 보이지만 수정하거나 사용할 수 없는 상태임을 표시한다.
- aria-grabbed: 드래그-드롭 기능의 'grabbed' 상태를 표시한다.

UI 위젯 요소의 상태를 표시하기 위해 ARIA state를 사용하고 요소의 클래스 이름을 바꾸기 위해 스크립트를 이용하는 대신에 상태 변경에 따른 시각적 표현을 바꾸기 위해 CSS 속성을 사용해야 한다.

예시1) 선택가능한 메뉴 HTML
```html
<ul id="fontMenu" class="menu" role="menu" aria-hidden="true">
    <li id="sans-serif"
        class="menu-item"
        role="menuitemradio"
        tabindex="-1"
        aria-controls="st1"
        aria-checked="true">
        Sans-serif</li>
    <li id="serif"
        class="menu-item"
        role="menuitemradio"
        tabindex="-1"
        aria-controls="st1"
        aria-checked="false">
        Serif
    </li>
```

예시2) 상태를 표현하기 위한 속성 기반의 선택자
```css
li[aria-checked="true"] {
    font-weight: bold;
    background-image: url('images/dot.png');
    background-repeat: no-repeat;
    background-position: 5px 10px;
}
```
위의 예시는 선택된 아이템의 시각적 모습을 변경하기 위한 CSS이다. 커스텀 클래스명이 없고 **aria-checked**의 상태만이 있다는 점이 주목할 만 하다.

예시3) aria-checked 속성을 변경하기 위한 자바스크립트
```javascript
var processMenuChoice = function (item) {
    item.setAttribute('aria-checked', 'true');
    
    var sib = item.parentNode.firstChild;
    for (; sib; sb = sib.nextSibling) {
        if (sib.nodeType === 1 && sib !== item) {
            sib.setAttribute('aria-checked', 'false');
        }
    }
}
```

### visibility 변경

컨텐츠의 visibility가 변경되었을 때(요소가 숨겨지거나 보이는 등), **aria-hidden** 속성값을 변경해주어야 한다.
위에서 묘사된 기법에서 요소를 숨기기 위해서는 `display:none`을 CSS 속성을 사용해야 한다.

