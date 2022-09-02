# Vue 싱글 파일 컴포넌트

1. Node.js 설치
2. Vue CLI 전역 설치
    
    ```powershell
    npm install -g @vue/cli
    ```
    
    -g: 로컬 어디서든 vue-cli를 요청할 수 있도록 함
    
3. vue 프로젝트 생성
    
    ```powershell
    vue.cmd create [프로젝트명]
    ```
    
    Please pick a preset에서 방향키를 이용하여 두 가지 선택지 중에 하나를 선택할 수 있는데, Default로 설정
    
    프로젝트의 node_modules 경로에 Babel, ESLint가 포함되어 있는 것을 볼 수 있음
    
    | Babel | 자바스크립트 컴파일러
    최신 버전의 자바스크립트 문법은 브라우저가 이해하지 못하기 때문에 Babel은 이 브라우저가 이해할 수 있는 구버전 문법으로 변환시켜줌 |
    | --- | --- |
    | ESLint | 코딩 스타일 가이드를 따르지 않거나 문제가 있는 코드나 안티 패턴을 찾아 표시를 달아놓는 도구 |
4. vue router 설치
    
    ```powershell
    npm install vue-router --save
    ```
    
    package-lock.json 파일에 router 내용이 추가된 것을 확인
    
    package.json 파일에 router 내용 추가된 것을 확인
    
5. 프로젝트 실행
	1. 프로젝트 경로로 이동
        
        ```powershell
        cd .\[프로젝트명]
        ```
        
    2. 실행
        
        ```powershell
        npm run serve
        ```
        
        `ctrl + c`를 이용해서 실행중인 서버 종료 가능
        
6. 확인
    
    브라우저 URL 탭에서 localhost:8080을 입력하여 이동한 페이지가 나타나면 프로젝트 생성 및 실행 성공
    
    * **디렉터리 구조**
    
    App.vue 가장 최상위 컴포넌트
    
    main.js 가장 먼저 실행되는 javascript 파일. Vue 인스턴스를 생성


<br><br><br>
    

# Vuex

vuex는 vue.js 애플리케이션을 위한 **상태 관리** 라이브러리이다. 모든 컴포넌트들에서 접근 가능한 중앙 집중식 데이터 저장소이다. 모든 데이터 흐름을 중앙에서 관리함으로써 예측 가능한 애플리케이션을 구현할 수 있다. Vue의 공식 devtools 확장 프로그램과 통합해서 사용하면 훨씬 사용하기 쉬워진다.

<br>

**상태 관리(State Management)가 필요한 이유**

컴포넌트 기반 프레임워크에서는 작은 단위로 쪼개진 여러 개의 컴포넌트로 화면을 구성한다. 예를 들면, header, button, list 등의 화면 요소가 각각 컴포넌트로 구성되어 한 화면에서 많은 컴포넌트를 사용한다. 이에 따라 컴포넌트간의 통신이나 데이터 전달을 좀 더 유기적으로 관리할 필요성이 생긴다.

<br>

**상태 관리란?**

상태 관리란 여러 컴포넌트 간의 데이터 전달과 이벤트 통신을 한 곳에서 관리하는 패턴을 의미

```powershell
npm install vuex --save
```

<br>

**Vuex 스토어 연동**

Vue 애플리케이션에서 Vuex 스토어를 사용하기 위해 전역 스토어를 생성하고 전역 Vue 인스턴스에 스토어를 주입시킨다. 루트 인스턴스에 store 옵션을 제공함으로써 저장소는 루트의 모든 하위 컴포넌트에 주입되고 this.$store로 스토어를 사용할 수 있다.

```jsx
// main.js
import Vue from 'vue'
import App from './App.vue'
import Vuex from 'vuex'
Vue.use(Vuex)

// 예시를 들기 위한 전역 스토어 객체
const store = new Vuex.Store({
	state: {
		count: 0
	},
	mutations: {
		increment (state) {
			state.count++
		}
	}
})

Vue.config.productionTip = false

new Vue({
	store, // store를 전역으로 등록
	render: h => h(App),
}).$mount('#app')
```

<br>

**상태 관리로 해결할 수 있는 문제점**

상태 관리는 중대형 규모의 웹 애플리케이션에서 컴포넌트 간에 데이터를 더 효율적으로 전달할 수 있다. 일반적으로 앱의 규모가 커지면서 생기는 문제점들은 다음과 같다.

1. 뷰의 컴포넌트 통신 방식인 props, event emit 때문에 중간에 거쳐야할 컴포넌트가 많아지거나
2. 이를 피하기 위해 Event Bus를 사용하여 컴포넌트 간 데이터 흐름을 파악하기 어려운 것

이러한 문제점을 해결하기 위해 모든 데이터 통신을 한곳에서 중앙 집중식으로 관리하는 것이 상태관리이다.

![Untitled](https://user-images.githubusercontent.com/80576569/188105343-9fecce25-2241-4be2-998d-858ea5907bd3.png)

- 상태(State)
- 변이(Mutation)
- 액션(Actions)

<br><br>

## 상태(State)

Vuex는 단일 상태 트리(단일 객체)를 사용. 애플리케이션에서 사용하는 하나의 원본 데이터라고 생각하면 된다. 애플리케이션의 모든 컴포넌트들은 데이터가 필요할 때, 이 원본 데이터를 꺼내서 사용

장점은 애플리케이션에서 사용하고 있는 데이터 흐름을 추적하기 매우 쉽다는 것이다. 언제 어떤 데이터가 변이했는지 알 수 있고, 시간 여행 디버깅을 할 수 있다.

- State를 Vue 컴포넌트에서 사용하기
    
    Vuex의 스토어의 state에 접근해서 Vue 컴포넌트의 계산된 속성(computed)에 주입만 시켜주면 됨
    
    ```jsx
    <script>
    export default {
    	name: 'App',
    	computed: {
    		count() {
    			return this.$store.state.count // store count 상태값
    		}
    	}
    }
    </script>
    ```
    
    this.$store.state.count의 상태값이 변경되면 자동으로 계산된 속성이 자동으로 변경되고 관련 DOM이 업데이트 될 것이다.


<br><br>

## 변이(Mutations)

변이(Mutations)는 Vuex 스토어(Store)에 있는 상태(State)값을 변경하는 유일한 방법이다. 변이를 사용하는 방법은 아래와 같다.

1. 변이 핸들러 생성
    
    ```jsx
    const store = new Vuex.Store({
    	state: {
    		count: 0,
    	},
    	mutations: {
    		// count 상태값을 증가시키는 변이
    		increment(state) {
    			state.count++;
    		},
    		// count 상태값을 감소스키는 변이
    		decrement(state) {
    			state.count++;
    		},
    	},
    });
    ```
    
2. 스토어(store)의 commit 메서드로 변이 핸들러 호출
    
    변이 핸들러는 직접 호출하지 않고 스토어(store)의 commit 메서드를 사용해서 호출한다. commit 메서드를 사용해서 변이 핸들러를 호출하는 방법은 다음과 같다.
    
    ```jsx
    this.$store.commit('increment') // 변이 핸들러 호출
    ```
    
    ```html
    <!-- 컴포넌트에서 store commit을 활용한 예시 -->
    <template>
    	<div id="app">
    		<button @click="$store.commit('increment')">증가</button>
    		<button @click="$store.commit('decrement')">감소</button>
    		{{ count }}
    	</div>
    </template>
    
    <script>
    export default {
    	name: "App",
    	computed: {
    		count() {
    			return this.$store.state.count++;
    		},
    	},
    };
    </script>
    ```
    

<br>

### 페이로드(payload)를 가진 커밋(commit)

commit 메서드를 실행할 때 페이로드(payload)라고 불리는 값을 전달할 수 있다. 페이로드는 상태 값을 변이 시킬 때 사용할 수 있다.

```jsx
...
mutations: {
	increment(state, n = 1) {
		state.count += n;
	},
}
```

```html
<!-- Vue 컴포넌트 -->
<button @click="$store.commit('increment', 3)">증가</button>
```

대부분의 경우 페이로드(payload)는 여러 필드를 포함할 수 있는 객체(Object)로 전달됨

```jsx
...
mutations: {
	increment(state, payload) {
		state.count += payload.amount;
	}
}
```

```jsx
this.$store.commit('increment', {
	amount: 10
})
```

<br>

### 객체(Object)스타일 커밋(commit)

변이를 커밋하는 또 다른 방법은 type 속성을 가진 객체를 직접 사용하는 것이다.

```jsx
this.$store.commit({
	type: 'increment',
	amout: 10
})
```

객체 스타일 커밋을 사용할 때 전체 객체는 변이 핸들러에 페이로드로 전달되므로 핸들러는 동일하게 유지됨

```jsx
mutations: {
	increment(state, payload) {
		state.count += payload.amount;
	}
}
```

```html
<!-- Vue 컴포넌트에서 사용 예시 -->
<button @click="$store.commit({type: 'increment', amount:3})">증가</button>
```

<br>

**!* 변이(Mutation)의 몇가지 중요한 팁**

Vue 반응성(Reactivity) 규칙을 따라야 한다.

Vuex 스토어의 상태값은 Vue에 의해 반응하므로, 상태값을 변경하면 상태값을 관찰하는 Vue 컴포넌트들이 자동으로 업데이트된다.

- 변경 감지할 데이터를 미리 초기화 함
- 만약 객체에 새 속성을 추가할 경우 다음 중 하나를 수행해야 함

Vue.set(object, key, value) 메서드를 사용하여 중첩된 객체에 반응성 속성을 추가함

```jsx
Vue.set(obj, 'newProp', 123)
```

객체를 새로운 객체로 교체한다. 예) 객체전개구문(ES6 spread operator)을 사용하면 아래와 같이 작성할 수 있다.

```jsx
state.obj = {...state.obj, newProp: 123}
```

<br>

**!* 반응성 예시**

countObj 객체에 a값은 미리 초기화를 했지만, b의 값은 컴포넌트의 마운트(mounted) 라이프 사이클 시점에 객체에 주입한 것을 알 수 있다.

```html
<template>
	<div id="app">
		<p>a: {{ countObj.a }}</p>
		<p>b: {{ countObj.b }}</p>
		<button @click="increment('a')">a 숫자 증가</button>
		<button @click="increment('b')">b 숫자 증가</button>
	</div>
</template>

<script>
export default {
	name: "App",
	data() {
		return {
			countObj: {
				a: 0,
			},
		};
	},
	mounted() {
		this.countObj["b"] = 0;
	},
	methods: {
		increment(type) {
			this.countObj[type]++;
		},
	},
};
</script>
```

countObj의 a 프로퍼티는 정상적으로 값이 변경되지만, countObj의 b 프로퍼티는 값이 변경되지 않는다.

Vm.$set 인스턴스 메서드를 사용해서 동적으로 객체에 반응성 속성을 추가

```jsx
export default {
	...
	mounted() {
		this.$set(this.countObj, "b", 0);
	}
}
```

객체에 동적으로 반응성 속성을 추가하고 컴포넌트가 제대로 업데이트 된다.

<br>

### 변이 타입(Mutation Type)으로 상수 사용을 지향함

변이(Mutation) 타입에 상수를 사용하는 것은 일반적인 패턴, 상수를 하나의 파일에 저장하면 같이 작업하는 팀원들이 전체 애플리케이션에서 어떤 변이가 가능한지 한 눈에 파악할 수 있다.

```jsx
// mutation-types.js
export const SOME_MUTATION = 'SOME-MUTATION'
```

```jsx
// store.js
import Vuex from 'vuex'
import {SOME_MUTATION} from './mutation-types'

const store = new Vuex.Store({
	state: {...},
	mutations: {
		[SOME_MUTATION] (state) {
			// 변이 상태
		}
	}
})
```

<br>

### 변이는 무조건 동기적이어야 함

변이의 필수적인 규칙은 변이 핸들러 함수는 동기적이어야 한다는 것이다. 비동기 흐름 처리는 액션(Actions)에서 처리한다.

<br><br>

## 액션(Actions)

액션은 액션 자체로 상태 값들을 변이 시키는 것이 아닌 모든 과정이 끝났을 때 변이에 대한 커밋(commit)을 시킨다. 변경을 확정 짓는 일을 커밋이라하며, 액션에서 모든 비동기 처리를 마치고 변이를 커밋함으로써 Vuex 스토어의 데이터를 업데이트한다.

*예) 액션과 변이를 적절하게 활용해서 비동기 흐름을 처리하고 데이터를 업데이트 하는 예시*

```jsx
// delay helper
const delay = (duration = 500) => {
	return new Promise((resolve) => {
		setTimeout(() => {
			resolve();
		}, duration);
	});
};

// 포스트 데이터를 가져오는 호출 예시 (비동기 호출)
const requestPostData = async (id = 0) => {
	await delay(1500);
	return [
		{
			id: 1,
			title: "post title 1",
			content: "post content 1",
		},
	];
};

// 유저 데이터를 가져오는 호출 예시 (비동기 호출)
const requestUserData = async () => {
	await delay(1500);
	return {
		id: 1317,
		name: "김김김",
		age: 30,
		url: "https://asd.com",
	};
};

const store = new Vuex.Store({
	state: {
		isLoading: false,
		posts: [],
	},
	mutations: {
		CHANGE_LOAD_STATUS(state, status = true) {
			state.isLoading = status;
		},
		SET_POST_DATA(state, posts) {
			state.posts = posts;
		},
	},
	actions: {
		async getUserPostData({ commit }) {
			try {
				commit("CHANGE_LOAD_STATUS"); // 로딩 처리 true
				const { id } = await requestUserData(); // 유저 데이터를 가져온다.
				const posts = await requestPostData(id); // 유저 데이터의 id 값으로 포스트 목록을 가져온다.
				commit("SET_POST_DATA", posts); // 포스트 데이터를 변이시키기 위해 커밋 메서드의 인자값으로 전달한다.
			} catch (err) {
				// 예외가 발생 시 여기에 로직 추가
				console.error(err);
			} finally {
				commit("CHANGE_LOAD_STATUS", false); // 로딩 완료 처리 false
			}
		},
	},
});
```

Vue 컴포넌트에서는 store.dispatch(’getUserPostData’)를 실행만 하고, 모든 비즈니스 로직들은 Vuex에서 처리를 담당하고 있는 것을 알 수 있다. 철저히 Vue 컴포넌트에서는 데이터를 화면에 보여주는 역할을 하고 있다는 것을 알 수 있다.

```html
<!-- Vue 컴포넌트에서 사용 예시 -->
<template>
	<div id="app">
		<p v-if="isLoading">post 데이터를 가져오는 중입니다...</p>
		<ul v-else>
			<li v-for="post in posts" :key="post.id">{{ post.title }}</li>
		</ul>
	</div>
</template>

<script>
export default {
	name: "App",
	mounted() {
		this.$store.dispatch("getUserPostData");
	},
	computed: {
		isLoading() {
			return this.$store.isLoading;
		},
		posts() {
			return this.$store.posts;
		},
	},
};
</script>
```

<br><br>

## 게터(Getter)

Getters는 Vue 컴포넌트의 computed(계산된 속성)이랑 같다. 직접 수정하는 값이 아닌 상태 값을 활용해서 계산된 속성으로 사용된다.

```jsx
const store = new Vuex.Store({
	...
	getters: {
		postCount(state) {
			return state.posts.length;
		}
	}
})
```

getters에서는 state에 접근해서 계산된 속성을 만들 수 있다. Vue 컴포넌트에서 계산된 속성은 상태값이 변경되면 자동으로 계산된 속성들은 업데이트 된다. Vuex의 Getters도 마찬가지, state 값이 변경되면 자동으로 getter는 변경된다.

<br><br>

## 모듈화(Module)

Vuex는 모듈이라는 것을 제공해준다. Vuex 단일 스토어를 모듈 단위로 쪼갤 수 있다. 각 모듈들은 자체 상태, 변이, 엑션, 게터를 포함할 수 있다.

```jsx
const moduleA = {
	state: () => ({...}),
	mutations: {...},
	actions: {...},
	getters: {...}
}

const moduleB = {
	state: () => ({...}),
	mutations: {...},
	actions: {...},
}

const store = new Vuex.Store({
	modules: {
		a: moduleA,
		b: moduleB
	}
})
```

위 처럼 구성하는 방법보다 모듈을 파일로 관리하는 편이다.

main.js Vuex 스토어를 붙일 때는 store를 따로 관리하곤 한다.

```jsx
// main.js
import Vue from 'vue'
import store from './store' // store를 가져옴
import App from './App.vue'

Vue.config.productionTip = false;

new Vue({
	store,
	render: (h) => h(App),
}).$mount('#app');
```

```jsx
// ./store/index.js
import Vuex from 'vuex'
import Vue from 'vue'
Vue.use(Vuex);

const delay = (duration = 500) => {
	return new Promise((resolve) => {
		setTimeout(() => {
			resolve();
		}, duration);
	});
};

const requestPostData = async (id = 0) => {
	await delay(500);
	return [
		{
			id: 1,
			title: "post title 1",
			content: "post content 1",
		},
		{
			id: 2,
			title: "post title 2",
			content: "post content",
		},
		{
			id: 3,
			title: "post title 3",
			content: "post content 3",
		},
	];
};

const requestUserData = async () => {
	await dealy(1500);
	return {
	id: 1317,
	name: "김김김",
	age: 30,
	url: "https://~"
	};
};

export default new Vuex.Store({
	state: {
		isLoading: false,
		posts: [],
	},
	getters: {
		postCount(state) {
		return state.posts.length;
	},
},
	mutations: {
		CHANGE_LOAD_STATUS(state, status = true) {
			state.isLoading = status;
		},
		SET_POST_DATA(state, posts) {
			state.posts = posts;
		},
	},
	actions: {
		async getUserPostData({ commit }) {
			try {
				commit("CHANGE_LOAD_STATUS");
				const { id } = await requestUserData();
				const posts = await requestPostData(id);
				commit("SET_POST_DATA", posts);
			} catch (err) {
				console.error(err);
			} finally {
				기존에 Vuex root store에 존재하던 post 로직을 모듈로 분리함
				commit("CHANGE_LOAD_STATUS", false);
			}
		},
	},
});
```

기존에 Vuex root store에 존재하던 post 로직을 모듈로 분리함

```jsx
// ./store/modules/post.js
import { requestPostData, requestUserData } from "../../api/post"

// initial state
const state = () => ({
	isLoading: false,
	posts: [],
});

// getters
const getters = {
	postCount(state) {
		return state.posts.length;
	},
};

// mutations
const mutations = {
	CHAGE_LOAD_STATUS(state, status = true) {
		state.isLoading = status;
	},
	SET_POST_DATA(state, posts) {
		state.posts = posts;
	},
};

// actions
const actions = {
	async getUserPostData({ commit }) {
		try {
			commit("CHANGE_LOAD_STATUS");
			const { id } = await requestUserData();
			const posts = await requestPostData(id);
			commit("SET_POST_DATA", posts);
		} catch (err) {
			console.error(err);
		} finally {
			commit("CHANGE_LOAD_STATUS", false);
		}
	},
};

export default {
	namespaced: true, // 스토어 모듈의 핵심
	state,
	getters,
	actions,
	mutations,
};
```

스토어의 모듈 핵심은 아래 namespaced에 있다. 모듈이 독립적으로 사용되기를 원한다면 namespaced: true라고 네임스페이스를 명시해야한다.

```jsx
// store/index.js
import Vuex from "vuex";
import post from "./modules/post";
import Vue from "vue";

Vue.use(Vuex);

export default new Vuex.Store({
	modules: {
		post,
	},
});
```

```jsx
/* eslint-disable no-unused-vars */
// Intial state
const statd = () => ({
	comments: [],
});

// getters
// `getters`는 해당 모듈의 지역화된 getters
// getters의 4번째 인자를 통해서 rootGetters 사용 가능
const getters = {
	commentCount(state) {
		return state.comments.length;
	},
};

// mutations
const mutations = {
	CHANGE_LOAD_STATUS(state, status = true) {
		state.isLoading = status;
	},
	SET_COMMENT_DATA(state, comments) {
		console.log("SET_COMMENT_DATA");
		state.comments = [
			{
				id: 1,
				name: "comment 1",
				content: "commnet content 1",
			},
		];
	},
};

// actions
const actions = {
	setCommentData({ commit }) {
		commit("SET_COMMENT_DATA");
	},
};

export default {
	namespaced: true,
	state,
	getters,
	actions,
	mutations,
};
```
<br>

**!* 스토어의 구조**

store

└ modules

└ comment.js

└ post.js

└ index.js

<br>

```jsx
// /store/index.js
import Vuex frome "vuex";
import post from "./modules/post";
import comment from "./modules/comment"; // comment 모듈 추가
import Vue from "vue";

Vue.use(Vuex);

export default new Vues.Store({
	modules: {
		post,
		comment,
	},
});
```

post 모듈 스토어에서 comment 모듈 스토어에 있는 액션과 변이 사용해보기, post 모듈 스토어의 getUserPostData 액션에서 comment 모듈 스토어의 액션인 setCommentData를 실행한다. 하지만 다른 모듈에 접근하기 위해서는 dispatch에 root: true를 사용해야 됨.

```jsx
// actions
const actions = {
	async getUserPostData({
		dispatch,
		commit,
		getters,
		rootGetters,
		rootState,
		state,
	}) {
		dispatch("comment/setCommentData", null, { root: true }); // comment의 setCommentData 액션 함수 실행
		...
	},
};
```

commit 또한 dispatch와 동일.

```jsx
commit('comment/SET_COMMENT_DATA', null, { root: true }) // -> 'SET_COMMENT_DATA'
```

<br>

## 컴포넌트에 모듈을 바인딩하는 방법

Vuex 라이브러리에서 제공하는 mapState, mapGetters, mapActions 헬퍼를 createNamespacedHelper와 함께 사용하여 네임스페이스헬퍼를 사용할 수 있다.

```jsx
import { createNamespacedHelpers } from 'vuex'
const { mapState, mapGetters, mapActions } = createNamespacedHelper('posts');
```

```html
<!-- App.vue 컴포넌트 -->
<template>
	<div id="app">
		<p v-if="isLoading">post 데이터를 가져오는 중입니다...</p>
		<template v-else>
			<ul>
				<li v-for="post in posts" :key="post.id">{{ post.title }}</li>
			</ul>
			<p>{{ postCount }}개</p>
		</template>
	</div>
</template>

<script>
import { createNamespacedHelpers } from "vuex";
const { mapState, mapGetters, mapActions } = createNamespacedHelpers("post");
export default {
	name: "App",
	mounted() {
		this.getUserPostData();
	},
	computed: {
		...mapCommentState(["comments"]), // 모듈의 네임스페이스 헬퍼를 같이 사용하고 싶을 때
		...mapState(["isLoading", "posts"]),
		...mapGetters(["postCount"]),
	},
	methods: {
		...mapActions(["getUserPostData"]),
	}
}
</script>
```
<br>

- mapGetters
    
    Vuex에 내장된 helper 함수, 한 번 가독성이 올라간 코드를 더 직관적이게 작성할 수 있다.
    
    ```html
    <div id="app">
    	Parent Counter : {{ parentCounter }}
    </div>
    ```
    
    ```jsx
    import { mapGetters } from 'vuex'
    
    computed: {
    	...mapGetters({
    		parentCounter: 'getCounter' // getCounter는 Vuex의 getters에 선언된 속성이름
    	})
    }
    ```
    
    `...` 문법을 사용하려면 Babel stage-2 라이브러리 설치 및 babel preset에 추가가 필요하다.
    
- mapMutations
    
    ```jsx
    import { mapMutations } from 'vuex'
    
    methods: {
    	// Vuex의 Mutations 메서드명과 App.vue 메서드명이 동일할 때 [] 사용
    	...mapMutations([
    		'addCounter'
    	]),
    	// Vuex의 Mutations 메서드명과 App.vue 메서드명을 다르게 매칭할 때 {} 사용
    	...mapMutations({
    		addCounter: 'addCounter' // 앞addCounter는 해당 컴포넌트의 메서드를, 뒤addCounter는 Vuex의 Mutations를 의미
    	})
    }
    ```
    
- mapActions
    
    ```jsx
    import { mapActions } from 'vuex'
    
    export default {
    	methods: {
    		...mapActions([
    			'asyncIncrement',
    			'asyncDecrement'
    		])
    	}
    }
    ```
    
    *namespace가 적용됨에 따라 호출되는 경로도 변경되어야 한다. 호출하려는 함수 앞’모듈_이름/’을 추가해야 한다. ex) dispatch(user/addCount)*
    

<br><br>

## Vue Routers

일반적으로 뷰에서 화면이 전환될 때 전환하는 행위를 Route라고 표현, 라우팅 라이브러리로 Vue Routers 제공.

vue 라우터는 기본적으로 RootURL/#/{Router name}의 구조로 되어있고, `#`태그 값을 제외하고 기본 URL 방식으로 요청 때마다 index.html을 받아 라우팅 하려면 다음과 같이 사용한다.

```jsx
const router = new VueRouter({
	routes,
	mode: 'history'
})
```

**라우터 인스턴스 생성시 설정값**

- `String` mode: 기본 값은 Hash 모드 (history 모드를 사용하면 브라우저 히스토리 스택에 기록됨)
- `String` redirect: 리다이렉팅 (주로 메인페이지 등에 사용)
- `Array` routes: 페이지 라우팅 정보
    - `String` path: 페이지 경로 (url)
    - `Object` component: 해당 url 페이지에 사용할 Component
    - `Array` children: 중첩 라우팅을 위한 배열

<br>

**인스턴스 생성**

```jsx
// router/router.js
import Vue from 'vue';
import VueRouter from 'vue-router';
import Main from '../views/Main.vue';
import Info from '../views/Info.vue';

Vue.use(VueRouter);

const router = new VueRouter({
	mode: 'history', // 해시값 제거 방식
	routes: [
		{
			path: '/',
			redirect: '/home'
		},
		{
			path: '/home',
			component: Main
		},
		{
			path: '/Info',
			component: Info
		}
	]
});
```

```jsx
// main.js
import Vue from 'vue';
import App from './App.vue';
import { router } from './router/index.js';

new Vue({
	router,
	render: h => h(App),
}).$mount('#app')
```

<br>

**선언적 방식**

`<router-link :to=”path” replace>`: 페이지 이동 태그, 화면에서는 `<a>` 태그로 치환됨, replace를 사용할 경우 속성으로 넣어줌

<br>

**프로그래밍 방식**

- `router.push(’path)`
    
    ```jsx
    // login path를 가진 컴포넌트 페이지로 이동함
    this.$router.push('/login');
    ```
    
- `router.replace(’path’)`: 새로운 히스토리 항목에 추가하지 않고 현재 항목을 대체함
- `router.go(n)`
    
    ```jsx
    // 한 단계 앞으로 감. history.forward()와 동일
    router.go(1)
    
    // 한 단계 뒤로 감. history.back()과 동일
    router.go(-1)
    
    // 3단계 앞으로 감
    router.go(3)
    
    // 지정한 만큼의 기록이 없으면 자동으로 실패함
    router.go(-100)
    router.go(100)
    ```
    
    **!* `<a>` 태그 대신 `<router-link>`를 쓰는 이유**
    
    - history 모드와 hashbang 모드는 주소 체계가 달라서 `<a>` 태그를 사용할 경우 모드 변경시 주소값을 일일이 변경해줘야 한다. `<router-link>`는 변경할 필요가 없다.
        - hashbang(#!): URL에서 발견할 수 있는 특수문자 “#!” (국내에서 거의 사용 안함)
    - `<a>` 태그를 클릭하면 화면을 갱신하지만 `<router-link>`는 갱신 없이 화면을 이동할 수 있음
    
    **!* 참고: Vue 인스턴스 내부에서 라우터 인스턴스에 `$router`로 액세스 할 수 있다. `this.$router.push`를 사용할 수 있음.**
    

<br>

**routes 정의 방식의 차이**

```jsx
const routes = [
	{
		path: '/',
		name: 'Home',
		component: Home,
	},
	{
		path: '/about',
		name: About,
		component: () => import('../views/About/vue')
	},
];
```

Home Component와 About Component의 정의 방식이 다름. 가장 먼저, 사이트가 로딩될 때 생성된 컴포넌트들을 모두 불러옴 → 불러온 컴포넌트들은 사용자 요청에 맞게 하나씩 렌더링.

최초 접속시 로딩 시간이 길어지게 되는 문제점이 있지만, 사이트를 한 번 접속하고 나면 빠르게 다른 페이지를 접근할 수 있는 장점이 있음 → 하지만, 규모가 크다면 문제가 발생

<br>

[차이점]

- Home Component: 사이트를 최초 방문할 때 모든 컴포넌트를 가지고 오게하는 방식
- About Component: 사이트를 최초 방문과 상관없이 해당 경로에 접근했을 때 컴포넌트를 가지고오는 방식

<br><br>

## 새로고침시 상태 초기화 방지: vuex-persistedstate

```powershell
npm install vuex-persistedstate
npm install --dev node-pre-gyp
```

```jsx
// store/index.js
import Vue from "vue";
import Vuex from "vuex";
import createPersistedState from "vuex-persistedstate";
import modules from "./modules";

Vue.use(Vuex);

const store = new Vuex.Store({
	modules,
	plugins: [
		createPersistedState();
	]
})
```

위와 같이 설정 시 모든 store 값들이 전부 localstorage에 저장되게 된다.

<br>

**vuex-persistedstate 일부만 저장**

해결 방법으로 vuex-persistedstate는 원하는 store 값만 저장하도록 하는 option이 있다.

```jsx
const store = new Vuex.Store({
	modules: moduleName,
	plugins: [
		// 여기에 쓴 모듈만 저장됨
		createPersistedState({
			paths: ['moduleName'],
		});
	]
})
export default store;
```

moduleName과 같이 store에 저장할 값들을 읽어 modules라는 곳에 추가, index.js에서는 const store로 정의한 파일을 객체화하여 외부로 보냄. 가장 중요한 일부 모듈의 state만 localstorage에 저장.

<br>

**Secure Local Storage**

```jsx
import Vue from "vue";
import App from "./App.vue";
import Vuex from "vuex";
import createPersistedState from "vuex-persistedstate";
import modules from "./modules";
import SecureLS from "secure-ls";

const ls = new SecureLS({ isCompression: false });
Vue.use(Vuex);
Vue.config.productionTip = false;

const store = new Vuex.Store({
	modules,
	plugins: [
		createPersistedState({
			paths: ['moduleName'],
			storage: {
				getItem: (key) => ls.get(key),
				setItem: (key, value) => ls.set(key, value),
				removeItem: (key) => ls.remove(key)
			}
		})
	]
});
export default store;
```

`Secure-ls` 라이브러리를 가져오고, `ls` 로컬 저장소에서 항목을 가져온 뒤 설정하고, 제거할 수 있도록 개체를 만듦. → 저장된 것은 무엇이든 스크램블되어 아무도 브라우저 개발 콘솔을 볼 수 없음.
