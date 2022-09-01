# Vue의 라이프사이클

1. 인스턴스의 생성(Create)
2. 생성된 인스턴스를 화면에 부착(Mount)
3. 화면에 부착된 인스턴스의 내용 갱신(Update)
4. 인스턴스 소멸(Destroy)


<br>

### **beforeCreate**

인스턴스가 생성되고 나서 가장 처음 실행됨. 즉, 인스턴스 초기화 직후에 발생. 이 때, data, method, 속성이 정의되지 않아서 DOM의 data 및 method에 접근할 수 없음.

```jsx
<script>
export default {
	data() {
		return {
			value: 'dataValue'
		};
	},
	beforeCraete() {
		console.log('beforeCreate');
		console.log(this.value); // undefined
	}
}
</script>
```

<br>

### **created**

created훅에는 data를 추적하는 것이 가능할 뿐 아니라, props, method, computed, watch가 활성화되어 접근이 가능. 하지만 아직까지 DOM에 추가되지 않은 상태.

data에 직접 접근이 가능하다는 점에서 컴포넌트 초기에 외부에서 받은 값들을 data로 세팅해야 할 때 이 단계에서 하는 것이 가장 적절함.

```jsx
<script>
import { eventBus } from "@/main.js"
export default {
	props: ["prosValue"],
	data() {
		return {
			value: "hello",
			initValue: null
		}
	},
	create() {
		console.log("created");
		console.log(this.value); // hello
		eventBus.$on("sendValue", (value) => {
			console.log(value);
		}); // 이벤트 받기
		this.initValue = this.propsValue;
		// props value를 data에 정의
	},
};
</script>
```

<br>

### **beforeMount**

DOM에 부착하기 직전에 호출됨. 가상 DOM은 이미 생성이 되어있으나 실제 DOM에는 아직 부착되지 않은 상태. 이 단계에서는 render 함수가 호출되기 직전의 로직을 추가하면 좋음

<br>

### **mounted**

가상의 DOM의 내용이 실체 DOM에 부착된 이후에 실행되는 훅이기 때문에 $el을 사용하여 실제 DOM에 접근할 수 있음. 이는 화면 요소를 제어하는 로직을 수행하기 좋은 단계

mounted훅이 호출되었다고 모든 컴포넌트가 마운트 되었다고는 할 수 없음. 전체 렌더링이 된 상태에서 작업을 진행하기 위해서는 `$nextTick` 를 사용하면 됨.

```jsx
<template>
	<div>
		{{ this.title }}
		<ul>
			<li>{{ this.subjectOne }}</li>
			<li>{{ this.subjectTwo }}</li>
		</ul>
	</div>
</template>

<script>
import { eventBus } from "@/mains.js"
export default {
	data() {
		return {
			title: 'hello',
			subjectOne: 'lifeCycle',
			subjectTwo: 'eventBus',
		};
	},
	mounted() {
		this.$nextTick(() => {
			// 모든 화면이 렌더링 된 후 호출
			console.log('mounted');
			console.log(this.$el);
		});
	},
};
</script>
```

<br>

### **beforeUpdate**

컴포넌트에서 사용되는 data의 값이 변경되면 컴포넌트가 재렌더링을 하게 되는데, 그 때 가상 DOM으로 화면을 다시 그리기 전에 호출되는 단계임. 실제 DOM에 변화를 적용시켜야 할 때, 그 변화 직전에 호출되기 때문에 따로 렌더링을 추가로 호출하지 않음.

<br>

### **updated**

가상 DOM을 렌더링하고 실제 DOM이 변경된 이후에 호출되는 단계. 데이터가 변경되고 나서 가상 DOM으로 다시 화면을 그리고 나면 실행되는 단계. 만약 변경된 값들을 가진 DOM을 이용해 접근하고 싶다면 이때가 가장 적절함. updated훅에서 data를 수정하게 되면 또 update훅이 호출 될 수 있기 때문에 무한 루프에 빠질 수 있으니 주의

<br>

### **beforeDestroy**

인스턴스가 소멸되기 직전에 호출되는 단계. 이벤트 리스너를 해체하거나 이벤트 버스를 off 하는 등 인스턴스가 사라지기 전에 해야할 일들을 처리하는 것이 좋음. 아직 인스턴스에 접근할 수 있기 때문에 Vue 인스턴스의 데이터를 삭제해야 한다면 삭제할 수 있음

```jsx
<script>
import { eventBus } from "@/main.js"
export default {
	data() {
		return {
			ctrlKey: false,
		};
	},
	created() {
		eventBus.$on("sendValue", (value) => {
			console.log(value);
		}); // 이벤트 버스 받기
	},
	mounted() {
		document.addEventListener("keydown", this.watchCtrlKeyDown);
		// Key EventListener 등록 => watchCtrlKeyDown 함수 호출
	},
	beforeDestroy() {
		document.removeEventListener("keydown", this.watchCtrlKeyDown);
		// Key에 대한 EventListener 해지
		eventBus.$off("sendValue"); // 등록한 이벤터 버스 없앰
	},
	methods: {
		// ctrl키를 감시하는 method
		watchCtrlKeyDown(event {
			let key = window.event ? window.event.keyCode : event.keyCode;
			switch (key) {
				case 17:
					this.ctrlKey = true;
					break;
			}
		}
	}
}
</script>
```

<br>

### **destroyed**

인스턴스가 소멸된 이후에 호출되는 단계임. 속성에 접근할 수 없으며 만약 하위 컴포넌트를 가지고 있다면 그것 또한 제거됨.
