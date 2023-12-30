Var와 Let은 변수선언, Const는 상수선언

흔히 듣는 말: "Var는 사용하지 말고 Let과 Const를 사용하라!"
왜일까?

Let과 Const는 2015 ES6에서 탄생한 문법

### Var와 Let의 차이점

변수이기때문에 값을 변경할 수 있지만

1. 스코프(Scope)
2. 중복 선언(Variable redeclaration)
3. 호이스팅(Hoisting)

에서 차이가 있다.

---

### 스코프(Scope)

: 코드가 변수에 접근할 수 있는 범위

1. Function Scope(함수 범위) : Var
2. Block Scope(블록 범위) : Let
3. Global Scope(전역 범위) : 어디에도 속하지 않는 최상위 함수 외부에서 선언된 변수라면 글로벌 스코프를 가짐

```
function soy() {
  if (true) {
   let a = '안녕';
   }
   console.log(a);
   }

 soy();
```

참조 에러가 뜸, 함수 스코프가 아닌 블록 스코프기 때문에 if의 밖에 있어서 접근할 수 없음 - 안전장치
while, for, switch도 마찬가지.

```
function soy() {
  let a = '하이';
  if (true) {
   let a = '안녕';
   }
   console.log(a);
   }

 soy();
```

'하이'가 출력이 됨, 안녕은 블록 내부에서만 접근가능하기 때문

```
function soy() {
  var a = '안녕하세요'
  if (true) {
   var a = '안녕';
   }
   console.log(a);
   }

 soy();
```

'안녕'이 출력이 됨, 위의 a와 아래의 a가 같은 스코프에 있고 중복 선언이 가능하기 때문에 덮여씌워진다.

```
function soy() {
  for (let i =0; i<2; i++){
    console.log(i);
  }
}

soy();
```

0
1
이 출력됨

```
function soy() {
  for (let i =0; i<2; i++){
    console.log(i);
  }
 console.log(i)
}

soy();
```

0
1
참조에러

```
function soy() {
  for (var i =0; i<2; i++){
    console.log(i);
  }
 console.log(i)
}

soy();
```

0
1
2
i는 함수 스코프를 가지고 있고 ++가 되어 2가 되어서 for문을 빠져나온다고 해도 밖에서 접근가능하기때문에 에러나지 않는다.

```
var soy = 'Hi';
let salt = 'Hello';
console.log(window)
```

함수로 감싸져있지 않기 때문에 전역변수
윈도우 객체 : 공유되는 단 하나밖에없는 전역객체
var는 윈도우에 등록이 되기 때문에 출력되지만 let은 등록되지 않아서 출력되지 않는다. var는 다른 값으로 덮여질 수도 있음 - 좋지 않은 경우

### 중복 선언

```
var a = '안녕';
var a = 'Hi';
console.log(a)
```

var키워드를 사용한다면 같은 이름을 가진 변수를 중복선언 가능 : Hi가 출력됨

```
let a = '안녕';
let a = 'Hi';
console.log(a);
```

let은 중복선언이 불가능 해서 이미 선언되었다는 에러가 뜸

### 호이스팅(Hoisting)

프로그램이 실행되기 이전에 변수의 선언과 초기화를 분리해서 변수의 선언부분을 프로그램의 맨 위로 끌어올려줌
즉, 프로그램이 실행되기 이전에 자바스크립트에게 사용하는 변수들의 존재를 미리 알려줌

- Var의 경우

```
console.log(a);
```

선언하지 않아서 ReferenceError가 일어남

```
console.log(a);
var a = 8;
```

undefined가 출력됨

```
console.log(a);
var a = 8;
console.log(a);
```

undefined
8
이 출력됨 : 변수의 선언과 추기화가 동시에 일어났지만 호이스팅으로 선언이 맨 위로 올라감

```
var a;
console.log(a);
a = 8;
console.log(a);
```

와 같은 경우가 됨, 자동으로 호이스팅되어 맨 위로 올라갈 때 undefined값으로 초기화됨
아무 값으로 초기화되지 않은, 값이 할당되지 않은 것에 접근을 한다는 것은 의미없는 일!

- let의 경우

```
console.log(a);
let a = 8;
console.log(a);
```

Reference Errorr가 일어남 초기화 되기 전에 접근할 수 없다.
호이스팅하지만 초기화시키지 않는다. undefined가 들어있지 않음.
: TDZ(Temporal Dead Zone, 일시적 사각지대)때문에
맨 위로 끌어올려지지만 코드상의 선언문에 닿기 까지는 TDZ에 들어가게 된다. 맨 위의 a는 TDZ에 있기 때문에 접근할 수 없음, 안전하게 코딩 가능 !

### Const

- Block Scope
- 중복 선언 불가
- 선언문 이전 접근 불가: 호이스팅시 초기화 하지 않기 때문
  let이 가지고 있는 장점을 가지고 있지만 변수가 아닌 '상수' 선언

한번 값을 할당하면 다른 값으로 재할당할 수 없음

```
const a = '안녕';
a = 'Hi';
```

다시 값을 할당할 수 없다는 에러가 발생함

상수의 특징 : 선언만 할 수 없다.
let은 let a;만 해도 가능하지만 나중에 a='1'로 할당해도 되기 때문.

```
const a;
```

초기화해야 한다는 에러가 뜸

```
const a;
a = '1';
```

에러가 뜸
또한 할당한 값이 숫자나 문자가 아니라 객체타입이라면 ?

```
const a = {
	x:0,
    y=1.
 };
 a = {a:2};
```

또 다른 값을 할당하려고 하면 에러가 뜸

```
const a = {
	x:0,
    y=1.
 };
 a.x=2;
```

가지고 있는 값을 바꾸려고 한다면 속성값이 바뀌고 에러가 뜨지 않음
가지고 있는 객체를 변경하는 것도 바뀌지 말고 불변성을 유지하려 한다면 ?

```
const a = Object.freeze({
	x:0,
    y=1.
 });
 a.x=2;
```

{x:0,y:1}로 출력이 됨

이렇게 const는 상수를 선언한다는 것외에는 let과 비슷하다.
