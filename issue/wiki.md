프로젝트 구조 설명
[MWS V22 프론트엔드 구조 설명 (Vue)] 2022-04-07 version
프로젝트를 실행하면 가장 먼저 App.vue가 실행되어 보여짐

main.js에서 사용할 라이브러리들을 설정해 놓을 수 있음 (사용할 bootstrap css 및 vue 라이브러리 등)

∗ src > api > internal과 private 폴더 존재
각 javascript파일 spring에 매핑 되어있는 주소로 request 작성 (vue와 spring을 연동하기 위함)

∗ src > store > modules
api는 module과 연동되어 데이터를 store에서 관리. 각 modules 사용하기 위해 vuex 라이브러리 사용. src > store > index.js에서 store 연동

module에는 각 항목 state, getters, mutations, actions가 존재

state : 원본 데이터를 의미. 직접적으로 사용하면 안됨

getters : 내부에 원본 데이터를 가져오는 getter 메서드 생성하면 됨

mutations : 원본 데이터를 변경할 때 사용. 원본 데이터를 변경하는 유일한 방법

actions : api를 호출하여 연동하고, 호출이 끝났을 때 mutations에 대한 커밋(변경을 확정짓는 일)을 시킴. 액션에서 모든 비동기 처리를 마치고 mutations을 적용함으로써 vuex 스토어의 데이터를 업데이트 함

∗ src > assets
웹에서 사용할 이미지들을 저장

∗ src > components
각 요소를 재사용할 수 있는 단위로 쪼개놓은 vue 파일. 페이지가 될 수도 있음. 그러나 많이 잘 쪼갤 수록 좋음

∗ src > filter
말 그대로 filter. 웹에 보여줄 데이터를 랜더링하기 위한 메서드 정의

∗ src > lang
홈페이지에서 지원할 언어 (영문/한국어) 를 json파일로 저장. 언어 랜더링 -> 요소에 사용될 이름 여기서 사용

∗ src > mixins
mixins에 등록된 메서드를 import하면, mixins가 먼저 적용되고 그 다음 사용자가 적용한 메서드가 적용됨

∗ src > router
매핑이 이루어지는 파일
최상위 src 경로부터~vue파일이 존재하는 경로까지 작성하여 import로 선언 후 -> routes 항목에서 path 및 이동할 컴포넌트 등록
∗ src > utils
공통적으로 javascript에서 사용할 메서드 정의

∗ src > views
각 모듈별 항목으로 vue 파일 정렬되어 있음
