# Vue.js의 CDN 사용 방식

```html
<!-- 개발 버전, 도움되는 콘솔 경고를 포함 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<!-- 상용 버전, 속도와 용량이 최적화 됨 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

<br>

### [01] Vue 인스턴스 만들기: new Vue

Vue 인스턴스는 SPA를 뒤에서 움직이게 하는 실체라고 볼 수 있음.

- **Vue 인스턴스 작성**
    
    ```html
    new Vue({Vue 인스턴스 내용})
    또는
    var 변수명 = new Vue({Vue 인스턴스 내용})
    ```
    
    - el 옵션
        
        어떤 HTML 요소와 연결할지를 지정함. HTML 중 `<태그명 id=”ID명”>`라는 요소를 작성해두고 el 옵션으로 el:”#ID명”으로 지정하는 것으로 그 요소와 연결됨.
        
    - data 옵션
        
        어떤 데이터가 있는지를 지정함. `data: {데이터 부분}`에서 데이터부분 영역에 `<프로퍼티명> : <값>` 과 같은 형식으로 작성, Vue.js에서는 데이터 이름을 프로퍼티라고 함. 만약 데이터가 복수라면 콤마로 구분하여 나열
        
    
    ```html
    <div id="ID명">
    </div>
    
    <script>
    	new Vue({
    		el: "#ID명",
    		data: { 프로퍼티명: 값, 프로퍼티명: 값 }
    	})
    </script>
    ```
    
- **그 외 Vue 인스턴스**
    
    ```jsx
    new Vue({
    	el: 어느 HTML 요소를 연결할 것인가
    	data: 어떤 데이터인가
    	methods: 어떤 처리를 하는가
    	computed: 어느 데이터를 사용하여 계산하는가
    	watch: 어느 데이터를 감시하는가
    })
    ```
    
<br>
<br>

### [02] 데이터를 그대로 표시: {{ 데이터 }}

- **이중 괄호({{}})로 표시**
    
    데이터를 있는 그대로 표시할 때는 {{데이터}} 사용. HTML의 텍스트 부분에 {{프로퍼티명}}이라고 작성. (머스태시)
    
- **v-text로 표시**
    
    Vue.js에서 기본적으로 HTML의 요소에 대해서 실행하는 명령은 디렉티브라고 함.
    
    요소에 대해서 Vue가 어떤 일을 하는지를 지정하는 명령어로써 앞에 `v-`가 붙어있음.
    
    ```html
    <태그명 v-text="프로퍼티명"></태그명>
    ```
    
- **v-html로 표시**
    
    머스태시나 v-text는 텍스트를 그대로 표시하지만 HTML로 표시하고자 할 때는 v-html을 사용함
    
    ```html
    <태그명 v-html="프로퍼티명"></태그명>
    ```
    
    - 주의 사항: HTML의 삽입으로 태그가 어긋난다던지 Javascript를 넣어 실행하는 것도 가능하므로 주의
    
<br>
<br>

### [03] 사용할 수 있는 데이터의 종류

- **기본적 데이터**
    
    숫자형, 문자형, 불린형 등
    
- **배열**
    
    배열에 값을 넣어두고 배열 자체를 다루거나 인덱스를 지정하며 배열 값에 접근할 수도 있음
    
- **오브젝트형**
    
    `Key와 Value의 한쌍`으로 오브젝트 데이터를 준비해두고 `<오브젝트명>.<키이름>` 으로 지정하면 값을 표시할 수 있음
    
- **미리 준비한 데이터 사용**
    
    Vue 인스턴스를 만들기 전에 Javascript로 만들어 놓은 데이터를 Vue 데이터로 읽어들여서 사용 가능
    
    ```html
    <div id="app">
    	<p>{{ myTea }}</p>
    	<p>{{ myTea[1].name }} {{ myTea[1].price }}원</p>
    </div>
    
    <script>
    	var teaList = [
    		{ name: "다즐링", price: 600 },
    		{ name: "얼그레이", price: 500 }
    	]
    	new Vue({
    		el: "#app",
    		data: {
    			myTea: teaList
    		}
    	})
    </script>
    ```
    
- **데이터의 내부를 확인하고 싶을 때**
    
    실제 데이터로 어떻게 읽어 들이고 있는지를 확인하고 싶을 경우에 $data를 사용. $data는 Vue 인스턴스에서 갖고 있는 모든 데이터를 말함.
    
    ```html
    <div id="app">
    	{{ $data }}
    	<li v-for="(item, key) in $data">{{ key }} : {{ item }}</li>
    </div>
    
    <script>
    	new Vue({
    		el: "#app",
    		data: {
    			myText: "Hello",
    			myNumber: 12345,
    			myBool: true,
    			myArray: [1, 2, 3, 4, 5]
    		}
    	})
    </script>
    ```
    

<br>
<br>

### [04] 요소의 속성을 데이터로 지정하는 : v-bind

데이터는 HTML 태그의 속성으로 사용하는 것도 가능하다. `v-bind 디렉티브` 사용

- **태그의 속성을 데이터로 지정**
    
    ```html
    <태그명 v-bind:속성="프로퍼티명"></태그명>
    ```
    
- **v-bind의 생략**
    
    v-bind는 자주 쓰이는 디렉티브로 생략 가능. `:` 만 사용해도 됨
    
    ```html
    <a v-bind:href="url"></a>
    <a :href="url"></a>
    ```
    
    - 이미지 지정하기
        
        img 태그의 src 속성의 파일명을 `data:`에 값으로 지정할 수 있음
        
        ```html
        <div id="app">
        	<img v-bind:src="fileName"></img>
        </div>
        
        <script>
        	new Vue({
        		el: "#app",
        		data: {
        			fileName: "test.png"
        		}
        	})
        </script>
        ```
        
    - 링크 지정
        
        a 태그의 링크를 `data:`의 프로퍼티로 URL을 지정할 수 있음. 배열로 준비된 링크들을 자동으로 나열하기 등의 용도로 사용할 수 있음
        
        ```html
        <div id="app">
        	<a v-bind:href="myURL"></a>
        </div>
        
        <script>
        	new Vue({
        		el: "#app",
        		data: {
        			myURL: "https://~"
        		}
        	})
        </script>
        ```
        
    - 인라인 스타일 지정 : style을 데이터로 지정
        
        ```html
        <p v-bind:style="프로퍼티명"></p>
        <p v-bind:style="{color:프로퍼티명}"></p>
        <p v-bind:style="{fontSize:프로퍼티명}"></p>
        <p v-bind:style="{backgroundColor:프로퍼티명}"></p>
        ```
        
    - 클래스 속성 지정
        
        ```html
        <p v-bind:class="프로퍼티명(클래스명)"></p>
        <p v-bind:class="[프로퍼티명(클래스명),프로퍼티명(클래스명)]"></p> <!-- class 복수 지정 -->
        <p v-bind:class="{'클래스명':프로퍼티명(true/false)}"></p> <!-- 데이터로 클래스 ON/OFF -->
        ```
        

<br>
<br>

### [05] 입력 폼을 데이터와 연결하기 : v-model

v-model 디렉티브는 input 태그, select 태그, textarea 태그 등을 사용

```html
<태그명 v-model="프로퍼티명"></태그명>
```

- **텍스트: input**
    
    input 태그의 텍스트를 Vue 인스턴스 데이터와 연결
    
    ```html
    <input v-model="프로퍼티명">
    ```
    
- **복수행 텍스트: textarea**
    
    textarea 태그의 텍스트를 Vue 인스턴스의 데이터와 연결, 입력하고 있는 중에도 갱신됨
    
    ```html
    <textarea v-mode="프로퍼티명"></textarea>
    ```
    
- **체크박스: input checkbox**
    
    값은 true/false 불린값. 체크박스 하나의 값을 데이터와 연결하는 것과 복수의 체크박스 값을 데이터와 연결할 수 있음.
    
    ```html
    <input type="checkbox" v-model="프로퍼티명">
    ```
    
    - 복수의 체크박스 값을 Vue 인스턴스의 데이터와 연결
        
        ```html
        <input type="checkbox" value="값1" v-model="동일한프로퍼티명">
        <input type="checkbox" value="값2" v-model="동일한프로퍼티명">
        <input type="checkbox" value="값3" v-model="동일한프로퍼티명">
        ```
        
        동일한 프로퍼티명으로 지정하면, 하나의 그룹으로 묶임
        
- **버튼: button**
    
    버튼의 활성/비활성을 데이터로 지정
    
    ```html
    <button v-bind:disable="프로퍼티명(true/false)"></button>
    ```
    
- **라디오 버튼: input radio**
    
    사용법은 복수의 체크박스와 비슷
    
    ```html
    <input type="radio" value="값1" v-model="동일한프로퍼티명">
    <input type="radio" value="값2" v-model="동일한프로퍼티명">
    <input type="radio" value="값3" v-model="동일한프로퍼티명">
    ```
    
- **선택: select**
    
    ```html
    <select v-model="프로퍼티명">
    	<option disabled value="">선택</option>
    	<option>선택값1</option>
    	<option>선택값2</option>
    	<option>선택값3</option>
    </select>
    ```
    
    복수의 선택값을 Vue 인스턴스의 배열 데이터로 연결할 수도 있음. 큰 차이점은 select 태그의 muitlple 속성
    
- **수식어**
    
    v-model에 수식어를 붙이면 몇가지 기능을 지정하는 것이 가능
    
    - 전부 작성하고 나서 Vue 인스턴스 데이터에 입력하고 싶을 때 : 입력한 후에 Enter 키를 누르거나 포커스를 이용하면 입력했던 문자열을 한꺼번에 출력
        
        ```html
        <input v-model.lazy="프로퍼티명">
        ```
        
    - 입력 내용을 자동으로 수식으로 변경하고 싶을 때
        
        ```html
        <input v-model.number="프로퍼티명">
        ```
        
    - 앞 뒤 공백을 자동으로 제거하고 싶을 때
        
        ```html
        <input v-model.trim="프로퍼티명">
        ```
        

<br>
<br>

### [06] 이벤트와 연결하기 : v-on

`v-on 디렉티브`는 유저가 버튼을 클릭하거나 키보드를 통해 키입력을 하는 등의 이벤트가 발생할 때 Vue 메서드를 실행시키는 이벤트 핸들러

```html
<태그명 v-on:이벤트="메서드명"></태그명>
```

메서드(명령문)는 Vue 인스턴스에 methods 옵션을 추가해서 생성

```jsx
new Vue({
	el: "#ID명",
	data: {
		프로퍼티명: 값,
		프로퍼티명: 값
	},
	methods: {
		메서드명: function () {
			// 처리 내용
		},
		메서드명: function () {
			// 처리 내용
		}
	}
})
```

- **v-on의 생략**
    
    v-on은 자주 사용되는 디렉티브이므로 생략할 수 있다. v-on 대신에 `@`을 사용하고 생략함
    
    ```html
    <a v-on:click="doSomething"></a>
    <a @click="doSomething"></a>
    ```
    
    - 버튼을 클릭했을 때
        
        ```html
        <button v-on:click="메서드명"></button>
        ```
        
    - 파라미터를 전달하여 메서드 실행
        
        ```jsx
        new Vue({
        	methods: {
        		메서드명: function (params) {
        			// 처리 내용
        		}
        	}
        })
        ```
        
- **키 입력**
    
    ```html
    <input v-on:keyup.키수식자="메서드명">
    ```
    
    키 수식자를 지정하지 않으면 아무키나 입력해도 메서드가 실행되어 버리게 되므로 특정 키를 입력했을 때만 반응하도록 키 수식자를 지정해야 함
    
    ```
    .enter
    .down
    .tab
    .left
    .delete
    .right
    .esc
    .48~57(0~9)
    .space
    .65~90(A~Z)
    .up
    ```
    
    이벤트에 시스템 수식자 키를 추가하면 시스템 키를 누르며 다른 키가 눌렸을 때만 메서드를 호출할 수 있게됨
    
    ```
    .ctrl
    .alt
    .shift
    .meta (Windows는 [Window]키, macOS는 [command]키)
    ```
    

<br>
<br>

### [07] 조건과 반복의 사용

- **배열의 데이터를 리스트로 표시**
    
    ```html
    <div id="app">
    	<ul>
    		<li v-for="item in myArray">{{ item }}</li>
    	</ul>
    </div>
    
    <script>
    	new Vue({
    		el: '#app',
    		data: {
    			myArray: ['짬뽕', '메론빵', '크로와상']
    		}
    	})
    </script>
    ```
    
- **오브젝트 배열 데이터를 리스트로 표시**
    
    ```html
    <div id="app">
    	<ul>
    		<li v-for="item in objectArray">{{ item.name }} ￦{{ item.price }}</li>
    	</ul>
    </div>
    
    <script>
    	new Vue({
    		el: "#app",
    		data: {
    			objArray: [
    				{name: '짬뽕', price: 1000},
    				{name: '메론빵', price: 1200},
    				{name: '크로와상', price: 1500},
    			]
    		}
    	})
    </script>
    ```
    
- **숫자 반복 표시**
    
    ```html
    <div id="app">
    	<ul>
    		<li v-for="n in 10">{{ n }}x 5 = {{ n * 5 }}</li>
    	</ul>
    </div>
    
    <script>
    	new Vue({
    		el: "#app"
    	})
    </script>
    ```
    
- **배열 데이터를 번호가 붙어있는 리스트로 표시**
    
    ```html
    <div id="app">
    	<ul>
    		<li v-for="(item, index) in myArray">{{ index }} : {{ item }}</li>
    	</ul>
    </div>
    
    <script>
    	new Vue({
    		el: "#app",
    		data: {
    			myArray: ["짬뽕", "메론빵", "슈크림빵"]
    		}
    	})
    </script>
    ```
    
- **버튼으로 리스트 추가/삭제**
    
    ```html
    <div v-for="item in myArray">
    	<ul>
    		<li v-for="item in myArray">{{ item }}</li>
    	</ul>
    	<button v-on:click="addList">맨 뒤에 추가</button>
    	<button v-on:click="addObj(3)">네번째에 추가</button>
    	<button v-on:click="changeObj(0)">첫번째를 변경</button>
    	<button v-on:click="deleteObj(1)">두번째를 삭제</button>
    </div>
    
    <script>
    	new Vue({
    		el: "#app",
    		data: {
    			myArray: ["첫번째", "두번째", "세번째", "네번째", "다섯번째"]
    		},
    		methods: {
    			addLast: function () {
    				this.myArray.push("[맨 뒤에 추가]");
    			},
    			addObj: function (index) {
    				this.myArray.splice(index, 0, "[추가]");
    			},
    			changeObj: function (index) {
    				this.myArray.splice(index, 1, "[변경]");
    			},
    			deleteObj: function (index) {
    				this.myArray.splice(index, 1);
    			}
    		}
    	})
    </script>
    ```
    
- **버튼을 클릭하면 정렬**
    
    ```html
    <div id="app">
    	<ul>
    		<li v-for="item in myArray">{{ item }}</li>
    	</ul>
    	<button v-on:click="sortData(myArray)">정렬</button>
    </div>
    
    <script>
    	new Vue({
    		el: "#app",
    		data: {
    			myArray: ["one", "two", "three", "four", "five"]
    		},
    		methods: {
    			sortData: function (listdata) {
    				listdata.sort(function (a, b) {
    					return (a < b ? -1 : 1)
    				});
    			}
    		}
    	})
    </script>
    ```
    

<br>
<br>

### [08] 데이터를 사용한 별도 계산: 산출 프로퍼티

```html
<p>{{ myPrice * 1.08 }}</p>
<p>{{ "안녕하세요" + myName + "님" }}</p>
<p>{{ myName.substr(0,1) }}</p>
```

데이터 값을 그대로 사용해도 좋지만 HTML만 보고 무엇을 표시하려고 하는지를 알 수 있어야 좋음

```html
<p>{{ taxIncluded }}</p>
<p>{{ sayHello }}</p>
<p>{{ nameInitials }}</p>
```

computed 옵션은 머스태시 태그 안에 쓰는 것과 달리 몇줄이라도 작성하는 것이 가능하므로 복잡한 처리를 작성할 수도 있음.

Vue의 인스턴스의 `data:`, `methods:`에 이어서 `computed: {computed프로퍼티명}`과 같이 씀. 그 안에는 `computed프로퍼티명:function(){처리내용}`과 같은 형식으로 추가함. 복수일 경우 컴마(,)구분으로 연결해서 사용할 수 있음

- **산출 프로퍼티 작성**
    
    ```jsx
    new Vue({
    	el: "#ID명",
    	data: {
    		프로퍼티명: 값,
    		프로퍼티명: 값
    	},
    	computed: {
    		computed프로퍼티명: function () {
    			// 처리 내용
    		},
    		computed프로퍼티명: function () {
    			// 처리 내용
    		}
    	}
    })
    ```
    
    ```html
    <div id="app">
    	<input v-model.number="price" type="number">원
    	<input v-model.number="count" type="number">개
    	<p>합계 {{ sum }}원</p>
    	<p>세금 포함 {{ taxIncluded }} 원</p>
    </div>
    
    <script>
    	new Vue({
    		el: "#app",
    		data: {
    			price: 100,
    			count: 1
    		},
    		computed: {
    			sum: function () {
    				return this.price * this.count;
    			},
    			taxIncluded: function () {
    				return this.sum * 1.08;
    			}
    		}
    	})
    ```
    

<br>
<br>

### [09] 표시/비표시 때의 애니메이션 효과: transition

1. 나타날(혹은 사라질) HTML 태그를 transition 태그로 감싼다.
2. 어떻게 변화할지를 CSS로 준비한다.
- **나타날(혹은 사라질) HTML태그를 transition 태그로 감싸기**
    
    `v-if`를 이용해서 나타날 HTML 태그를 준비하고, transition 태그로 감싼다.
    
    ```html
    [단일 태그의 트랜지션]
    <transition>
    	<div v-if="isOK">표시/비표시의 변경</div>
    </transition>
    ```
    
- **어떻게 변화할지를 CSS로 준비**
    
    ```html
    [CSS 스타일]
    * 태그가 나타날 때
    - .v-enter : 나타나기 전의 상태
    - .v-enter-action : 나타나고 있는 상태
    - .v-enter-to : 나타난 상태
    
    * 태그가 사라질 때
    - .v-leave : 사라지기 전의 상태
    - .v-leave-active : 사라지고 있는 상태
    - .v-leave-to : 사라진 상태
    
    * 태그가 이동할 때
    - .v-move : 태그가 이동할 때
    ```
    
    ```css
    .v-enter {
    	opacity: 0;
    }
    .v-enter-active {
    	transition: 1s;
    }
    ```
    
    나타난 상태(.v-enter-to)는 기본 상태이므로 설정하지 않음
    

<br>
<br>

### [10] 리스트의 트랜지션: transition-group

리스트의 수가 증감하거나 위치가 이동될 때 애니메이션 효과를 줄 수 있음. 리스트의 경우는 transition-group 태그로 감싼다. 이 때, Vue가 태그의 어디를 증가시키는지(삭제하는지), 어디로 이동한느지 등을 추적할 수 있도록 각각 다른 값을 `v-bind:key=”다른값”`으로 지정할 필요가 있음

```html
[리스트의 트랜지션]
<transition>
	<li v-for="item in dataArray" v-bind:key="item">{{ item }}</li>
</transition>
```

<br>
<br>

### [11] 컴포넌트

HTML에서 컴포넌트명의 태그를 쓰면 그 부분에 준비된 컴포넌트가 표시됨

```html
<my-component></my-component> <!-- 준비된 컴포넌트가 표시됨 -->
```

컴포넌트를 만드는 방법 1. 글로벌로 등록하는 방법, 2. 로컬에 등록하는 방법

- **글로벌에 등록하는 방법**
    
    Vue.component를 사용해서 컴포넌트를 만들면 글로벌에 등록되어 그 이후에는 작성되는 Vue 인스턴스에서도 사용 가능
    
    ```jsx
    Vue.component('컴포넌트태그명', {
    	template: 'HTML 부분'
    })
    ```
    
- **로컬에 등록하는 방법**
    
    ```jsx
    var 컴포넌트의오브젝트명 = {
    	template: 'HTML 부분'
    }
    
    new Vue({
    	el: "#app",
    	components: {
    		'컴포넌트태그명': 컴포넌트의 오브젝트명
    	}
    })
    ```
    
    ```html
    <div id="app">
    	<my-component></my-component>
    	<my-component></my-component>
    	<my-component></my-component>
    </div>
    <script>
    	var MyComponent = {
    		template: '<p class="my-comp">Hello</p>'
    	}
    
    	new Vue({
    		el: "#app",
    		components: {
    			'my-component': MyComponent
    		}
    	})
    </script>
    ```
    

<br>
<br>

### [12] 컴포넌트의 data를 function으로 만들기

```jsx
[컴포넌트의 data]
data: function () {
	return {
		프로퍼티명: 값
	}
}
```

<br>
<br>

### [13] 값 전달: props

```jsx
props: function () {
	프로퍼티명: 값
}
```

props 옵션 중 프로퍼티 평균은 myName과 같이 카멜케이스 사용, HTML 태그 안에는 my-name과 같이 케밥케이스 사용.

props 옵션에서 HTML의 태그로부터 전달하는 것이 가능하게 되었지만, 확실히 전달되었는지 되지 않았는지 체크할 필요가 있음. `create:`을 사용해서 인스턴스가 만들어진 직후 타이밍에 실행하는 것이 가능함. 값이 전달되었는지를 체크할 수 있음.

```jsx
create: function () {}
```

```jsx
Vue.Component('todo-item', {
	// todo-item 컴포넌트는 "prop"이라고 하는 사용자 정의 속성 같은 것을 입력받을 수 있음.
	// 이 prop은 todo라는 이름으로 정의
	props: ['todo'],
	template: '<li>{{ todo.text }}</li>'
})
```

`v-bind`를 사용하여 각각 반복되는 `todo-item` 컴포넌트에 전달할 수 있음

```html
<div id="app-7">
	<ol>
		<!-- 각 todo-item에 todo 객체를 제공
					화면에 나오므로 각 항목의 컨텐츠는 동적으로 바뀔 수 있음.
					또한, 각 구성 요소에 "키"를 제공해야 함. -->
		<todo-item
			v-for="item in groceryList"
			v-bind:todo="item"
			v-bind:key="item.id"
		>
		</todo-item>
	</ol>
</div>
```

```jsx
Vue.component('todo-item', {
	props: ['todo'],
	template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
	el: "#app-7",
	data: {
		groceryList: [
			{ id: 0, text: 'Vegetables' },
			{ id: 1, text: 'Cheese' },
			{ id: 2, text: 'Whatever else humans are supposed to eat' },
		]
	}
})
```

```
[출력 결과]
1. Vegetables
2. Cheese
3. Whatever else humans are supposed to eat
```
