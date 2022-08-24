# ES6 문법, ES5와의 차이점

ES란, ECMASCRIPT의 약어를 뜻하며, 자바스크립트의 표준, 규격을 나타내는 용어이다. 뒤에 숫자는 버전을 뜻하는데 ES5(2009년), ES6(2015년) 출시하였다.

ES6 이후에는 매년 업데이트가 되고 있는 반면, ES5와 ES6 사이에는 시간 차이가 있다. (6년) ES6+ (ES6 이후, 모던 자바스크립트라고 부름)

<br>

1. **let, const 키워드 추가**

기존의 var 키워드는 함수 레벨 스코프를 가지며 암묵적 재할당이 가능했다. 단점을 보완하기 위해 블록 레벨 스코프를 가지며 재할당이 가능한 let, const 키워드가 추가되었다.

<br>

2. **Arrow function 추가**

화살표 함수가 추가되어 함수를 간결하게 나타낼 수 있다. 가독성 및 유지 보수성이 올라갔다고 판단된다. 단, 기존의 함수와 this 바인딩아 다르다. 화살표 함수는 lexical this를 따르기 때문에 추가 공부가 필요하다. 화살표 함수에서는 매개변수가 하나일 때 괄호() 생략 가능, {} 및 return 도 생략 가능하다.

```jsx
// ES5
function sum(a, b) {
	return a + b;
}

// ES6
const sum = (a, b) => a + b;
```
<br>

3. **Default parameter 추가**

기존에 함수의 매개변수에 초깃값을 작성하려면 함수 내부에서 로직이 필요했으나 ES6 이후 default parameter가 추가되었다.

```jsx
// ES5
var bmi = function (height, weight) {
	var height = height || 184;
	var weight = weight || 84;
	return weight / (height * height / 10000);
}
// 함수 호출시 매개변수로 키와 몸무게를 할당하면, bmi를 리턴해주는 함수 작성
// 파라미터가 없을 시 작성자의 bmi를 리턴

// ES6
const bmi = function (height = 184, weight = 84) {
	return weight / (height * height / 10000);
}
```

<br>

4. **Template Iiternal 추가**

ES6 이전 문자열 관리는 불편했다. Template Iiteral이 도입된 후 간편해졌다. 사용법은 ``(back tic)이다. ${} 중괄호 앞에 달러 표시를 통해 표현식을 삽입 가능하다. 공백을 이용하는 불편도 사라졌다.

```jsx
// ES5
var firstName = 'Seo';
var lastName = 'yerim';
var name = 'My name is ' + firstName + ' ' + lastName + '.';

// ES6
const myName = `My name is ${firstName} ${lastName}.`;
console.log(myName);
// My name is seo yerim

// ES5 공백의 불편함
console.log('방문해' + ' ' + '주셔서' + ' ' + '감사합니다.');

//ES6 공백 있는 그대로 인식
console.log(`방문해 주셔서 감사합니다.`);
```
<br>

5. **Multi-line string**

문자열이 라인을 넘어가게 되면 관리가 불편했다. `\n` 줄바꿈과 덧셈 연산자를 사용해야 했다. 백틱을 사용하면 여러 라인의 문자열도 문제없다.

```jsx
// ES5
var lorem = 'Lorem ipsum dolor sit amet, consecteur adipiscing elit.\n' +
	'Aliquam ligula sapien, rutrum sed vesttibulum eget.\n';

// ES6
var lorem = `Lorem ipsum dolor sit amet, consecteur adipiscing elit.
	Aliquam ligula sapien, rutrum sed vesttibulum eget.`;
```
<br>

6. **Class**

객체 생성 방식 중 하나이며, 자바스크립트는 프로토타입 기반의 객체지향 프로그래밍이다. ES5에서는 클래스라는 키워드가 없었지만 프로토타입을 통해 실현 가능 했다.

```jsx
// ES5
var Add = function(arg1, arg2) {
	this.arg1 = arg1;
	this.arg2 = arg2;
};
Add.prototype.calc = function() {
	return this.arg1 + '+' + this.arg2 + '=' + (this.arg1 + this.arg2);
};
var num = new Add(5, 8);
console.log(num.calc()); // 5 + 8 = 13

// ES6
class Add {
	constructor(arg1, arg2) {
		this.arg1 = arg1;
		this.arg2 = arg2;
	}
	calc() {
		return this.arg1 + '+' + this.arg2 + '=' + (this.arg1 + this.arg2);
	}
}
var num = new Add(5, 8);
console.log(num.calc()); // 5 + 8 = 13
```
<br>

7. 모듈

ES5 이전에는 각 기능별로 파일을 나누고 개발 및 관리하는 것이 불가능했다.

```html
// ES5
<script src="slider.js"></script>
<script src="script.js"></script>
```

```jsx
var slider = require(./slider.js)
```

위와 같이 사용함으로써 `slider.js`를 import 할 수 있었다. 이러한 방법으로 파일 자체를 사용할 수 있었다.

ES6 부터는 import/export로 모듈을 관리할 수 있다. 모듈은 실현 가능한 특정 프로그램의 그룹이다. 다른 파일의 변수, 함수를 참조한다.

<br>

***하나의 모듈만 공유할 때***

```jsx
// ES6
// - 로드 모듈
import 'import to loadName' from '파일 경로';

// - 아웃풋 모듈
export default 'module';
```

```jsx
import Carousel from './carousel';
const carousel = new Carousel();

export default class Carousel {
	constructor() {
		this.calc();
	}
	calc() {
		console.log(10);
	}
}
```

***여러 모듈을 사용할 때***

```jsx
import {a1, a2, ...} from '파일 경로';
import * as 'object name' from '파일 경로'; // 모든 모듈을 전달 받을 경우
import { multi, superMulti } from './Multiply';
console.log(multi(5)); // 50
console.log(superMulti(6)); // 600
```

```jsx
export const i = 10;
export function multi(x) {
	return i * x;
}
export function superMulti(x) {
	return i * x * 10;
}
```
<br>

8. Destructuring 할당

Destructuring이란 비구조화, 파괴를 뜻하는 단어이며 크게 객체나 배열에서 사용해서 개별 변수에 할당하는 것이다.

```jsx
// array destructuring
const arr = [1, 2, 3];
const [one, two, three] = arr;

// object destructuring
const obj = { firstName: 'seo', lastName: 'yerim' };
const { lastName, firstName } = obj;
```

우항에 존재하는 자료구조를 파괴하여 좌항에 있는 변수들에게 각각 할당하는 듯한 내용을 보여주게 되는데, 위의 예제에서 배열은 순서을 중요하게 여기게 되고, 객체는 키 값을 중요하게 여겨 순서를 바뀌어도 동일하게 동작한다(값만 추출). destructuring 할당을 통해 자료구조에서 일부 또는 전체를 편리하게 사용할 수 있다.

<br>

9. Promise

비동기 통신에 있어 기존에는 콜백 함수를 사용한 콜백 패턴을 사용했다. 결과론적으로 콜백헬을 발생시켰고, 이를 해결하기위해 Promise가 도입되며 Promise 후속 처리 메서드를 이용해 에러를 효과적으로 처리할 수 있게 되었다.

<br>

10.  string 메서드 (includes, startsWith, endsWith)

```jsx
const text = 'Hello world ~ yerim ~';
text.includes('yerim');   // true
text.startsWith('Hello'); // true
text.endsWith('~');       // true
```

true/false 값을 리턴하여 문자열 메서드들로 검사 로직을 수행할 수 있다.
