# DOM과 Virtual DOM

MDN에서는 DOM은 HTML, XML document와 상호작용하고 표현하는 API이다. DOM은 browser에서 로드되며, Node 트리(각 노드는 document의 부분을 나타낸다)로 표현하는 document 모델이다.

(ex: element, 문자열, 혹은 코멘트)

<br>

**.HTML 파일이 브라우저에 표현되는 과정**

1. 브라우저의 랜더링 엔진은 웹 문서를 로드한다.
2. 웹 문서를 로드한 후, 웹 문서를 브라우저가 이해할 수 있는 구조로 구성하여 메모리에 올린다.
3. 브라우저는 브라우저가 이해할 수 있는 구조를 그려낸다.

<br>

**브라우저가 이해할 수 있는 구조**

브라우저의 랜더링 엔진은 모든 요소(Element)와 속성(Attribute) 등을 각각의 객체로 만들고 이것을 트리구조로 구성한다. 이를 DOM이라고 한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7e277550-9528-4108-81c5-963968183bbf/Untitled.png)

<br>

**노드(Node)**

가장 일반적인 노드 유형(node type)은 다음과 같다.

- DOCUMENT_NODE (ex. `window.document`)
- ELEMENT_NODE (ex. `<html>, <body>, <a>, <p>, <script>, <style>, <h1>`)
- ATTRIBUTE_NODE (ex. `class=”hi”`)
- TEXT_NODE (ex. 줄바꿈과 공백을 포함한 HTML 문서 내의 텍스트)
- DOCUMENT *FRAGMENT*NODE (ex. `document.createDocumentFragment()`)
- DOCUMENT *TYPE*NODE (ex. `<!DOCTYPE html>`)

<br>

DOM은 브라우저에서 로드되는 것이다. 각자의 IDE에서 작성한 HTML은 DOM이 아니고, 작성된 HTML 문서가 브라우저에 의해 해석되어 실제 문서를 나타내는 노드 트리가 DOM이다. 그리고 이러한 DOM은 자바스크립트로 해당 문서에서 노드 추가, 삭제, 변경, 이벤트 처리, 수정 등을 가능케하는 API를 제공한다.

<br>

아무리 IDE에 HTML을 작성한다 한들 최종적으로 이 결과물을 보기 위해 브라우저가 필요하다. IDE에 작성된 HTML은 단순한 문자열(string)일 뿐이며, 브라우저가 이해하기 위해서는 노드(객체)로 변환해야 한다.

<br>

즉, DOM은 HTML과 자바스크립트를 이어주는 공간으로, 내가 작성한 HTML을 자바스크립트가 이해할 수 있도록 객체(object)로 변환하는 것이다.

<br>

**브라우저 동작 원리**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2fe598ee-d176-4b46-b292-e4f2ef1974c1/Untitled.png)

브라우저가 HTML을 전달 받으면, 곧 이를 변환(파싱)하고 노드들로 이루어진 DOM 트리를 만든다. 그 후 외부의 CSS 파일과 각 노드들의 inline 스타일을 파싱하여 스타일을 입힌 Render 트리를 만든다.

<br>

Render 트리가 만들어지면 각 노드들이 화면에서 정확히 어디에 나타나야 하는지에 대한 위치가 주어진다. 그 후 paint() 메서드를 호출하면 내가 구현하고 싶었던 화면이 출력된다.

<br>

DOM은 해당 과정을 계속 반복한다. 오타 수정, 문구 제거 혹은 이미지를 첨부하는 사소한 일을 하더라도 DOM은 처음부터 다시 HTML을 파싱하여 DOM 트리를 만들고, CSS를 파싱하여 Render 트리를 만들고, 레이아웃을 입혀 출력한다.

<br>

오타 하나를 잡기 위해서 전체 사이트를 다시 처음부터 렌더링(위의 결과물 출력 과정)을 해야하며 해당 오타를 찾기 까지 너무나 많은 시간이 들어가 상당히 비효율적이다.

<br><br>

## Virtual DOM

Virtual DOM(이하 가상 DOM)은 수정사항이 여러가지 있더라도 가상 DOM은 한 번만 렌더링을 일으킨다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7013f123-bb29-4619-b49d-fdeeac068998/Untitled.png)

위의 그림처럼 가상 DOM은 DOM이 생성되기 전, 이전 상태값과 수정사항을 비교하여 달라진 부분만 DOM에게 한 번에 전달하여 딱 한 번만 렌더링을 진행한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8f0307d8-cfcf-4856-8bb3-813cf98fca76/Untitled.png)

빨간 부분에 수정사항이 생겼다면, 가상 DOM이 알아서 달라진 값을 탐지하여 변경하고 최종적인 결과물을 실제 DOM에 전달한다. 만약 가상 DOM이 없었다면, DOM은 렌더링을 처음부터 해야했기 때문에 모든 원이 빨갛게 바뀌었을 것이다.

> 직접 DOM에 접근하는 것은 지양해야 한다.


이는 DOM에 직접 접근해도 문제가 되지 않지만, DOM이 직접 변경된다면 사소한 변경 사항에도 전체가 재렌더링 되기 때문에 브라우저에 과부하가 올 수 있다. 따라서 최대한 DOM에 접근하지 말아야 한다.

<br><br>

**가상 DOM이 해결해주는 것은?**

DOM 관리를 자동화하고 추상화하여 직접할 필요가 없게 해주는 것이다. 또한 전체 DOM Tree를 reload 하지 않기 위해 변경한 부분과 변경되지 않은 부분을 직접할 때는 추적해야 하나 이 또한 가상 DOM이 자동화 해주는 것이다. DOM 조작 자체를 포기함으로써 DOM을 수정하는 모든 부분 간의 동기화를 피할 수 있다.
