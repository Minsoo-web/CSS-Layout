# Variables

## 📖 index

- [let and const](#let-and-const)

### let and const

#### 🚀 intro

<p align="center">
    <image alt="var" src="../../images/es6/es6_var.jpg">
</p>

> var 는 더이상은 naver,,,

기존에 c++ 이나 java 와 같은 정적타입의 언어를 공부하시던 분들은 JS 를 공부하실때  
처음 느끼는 낯선 점이 바로 `var` 일 것입니다. 🤦

Array, Int, String, Char 등등 모든 타입을 프로그래머가 변수의 타입을 직접 명시해 주어야 하는 언어를  
`정적 타입 언어 (Statically typed language)` 라고 합니다.

python과 JS 처럼 우선 변수를 선언해서 코드를 작성한 뒤, 런타임에 타입이 결정되는 언어들을  
`동적 타입 언어(Dynamically typed language)` 라고 합니다.

이러한 _동적 타입의 언어_ 들이 갖는 장단점이 분명히 있지만 모든 것을 `var` 로 퉁쳐버리는 JS의 특징은 많은 개발자에게 불편함을 안겨주기도 했습니다.

그러한 니즈를 해결해줄 수 있는 것이 바로 `let`과 `const` 입니다.  
하나하나 살펴보겠습니다!

#### MDN Says

> 👨🏼‍⚖️ MDN:  
> `let` 구문은 **블록 유효 범위**를 갖는 지역 변수를 선언하며,  
> 선언과 동시에 임의의 초기 값으로 초기화할 수도 있다.

> 👨🏼‍⚖️ MDN:  
> `const` 선언은 **블록 범위**의 **상수**를 선언합니다.  
> 상수의 값은 **재할당할 수 없으며 다시 선언할 수도 없습니다.**

#### 블록 유효 범위란

프로그래밍 언어에서 변수는 참조할 수 있는 범위가 존재합니다.  
그래서 변수는 선언된 위치에 따라 유효 범위를 갖게 됩니다.  
`let`과 `var` 그리고 `const`가 갖고있는 유효 범위에 대해 알아보겠습니다.

1\. var - 함수 레벨 범위 (Function Level Scope)

`var` 키워드를 사용하여 변수를 선언하면, 그 변수는 함수 레벨 범위를 갖습니다.

```JavaScript
function foo(){
    if(true){
        var x = 10;
    }
    console.log(x);
}

foo(); // 10
console.log(x); // Error!
```

`foo()` 함수 내에서는 `x`가 어디서 쓰이든 참조가 가능하기 때문에  
`console.log(x)` 가 에러가 나지 않습니다. 하지만 `foo()` 함수 밖에서 `x`를 참조하게 될 경우에는  
유효 범위를 벗어난 곳에서 `x` 를 호출한 경우이므로 Error 가 발생하게 되는 것입니다.

만약 함수 밖에서 var 키워드를 통해 선언 되었다면 그 변수는 `Global Scope`가 됩니다.

2\. let, const - 블록 레벨 스코프 (Block Level Scope)

`let`, `const` 키워드를 사용하여 변수를 선언하면, 그 변수는  
`Block Level Scope` 를 갖습니다.

> _*Block Level*_ 이란 `{} 중괄호`로 감싸진 범위라고 생각하시면 됩니다.

두 키워드의 차이는 수정 여부인데, `const` 키워드를 통해 선언된 변수는  
_수정이 불가능합니다._

```JavaScript
if(true){
    let x=10;
    const y=10;
    y =12; // Error ! 수정 불가능!
}

// 블록 단위를 벗어났으므로 x,y를 모르는 상태가 됩니다.
console.log(x); // Error! x가 뭔데!
console.log(y); // Error! y가 뭔데!
```

#### let과 const의 특징

- let은 중복 선언이 안 된다.
- const는 수정이 안 된다.
- const는 선언과 동시에 초기화를 해야 한다.
- let과 const는 `Hoisting`이 되지 않는다.
- let을 통해 closure 이슈를 해결할 수 있다.

[Hoisting?](https://github.com/Minsoo-web/es_features/blob/master/etc/hoisting.md)  
[Closure?](https://github.com/Minsoo-web/es_features/blob/master/etc/closure.md)

#### 🏄‍♂️ 예제

##### let 의 중복선언

```JavaScript
var one = 1;
var one = 2;

let two = 2;
let two = 3; // SyntaxError: Identifier 'two' has already been declared
// 이미 선언 했다고 찡찡대는 우리의 let
```

##### const의 특징들

```JavaScript
// const 키워드의 변수는 수정이 불가!
const x=1;
x=2; // TypeError: Assignment to constant variable.

// const 키워드의 변수는 선언과 동시에 초기화를 해줘!
const y; // SyntaxError: Missing initializer in const declaration
y=1;
```

##### Hoisting

```JavaScript
// x 가 뭔데
console.log(x); // ReferenceError: Cannot access 'x' before initialization

let x = 10;

// PI가 뭔데
console.log(PI); // ReferenceError: Cannot access 'PI' before initialization

const PI = 3.14;
```

##### let을 통한 Closure 이슈 해결

```JavaScript
function count() {
    for (var i = 0; i < 10; i++) {
        setTimeout(() => {
            console.log(i); // 여기서 참조하는 i는 반복문을 다 돌고 난 다음의 i 이기 때문에 10이 됩니다.
        }, 0);
    }
}

count(); // 10만 열번 출력

```

위 코드에서 var 키워드를 let으로 변경하면  
0 ~ 9 까지 출력이 되는 것을 확인할 수 있습니다.

```JavaScript
function count() {
    for (let i = 0; i < 10; i++) {
        setTimeout(() => {
            console.log(i); // 여기서 참조하는 i는 블록 단위의 scope를 갖는 i이기 때문에
                            // 호출이 될 때의 i인 0 ~ 9가 됩니다.
        }, 0);
    }
}

count(); // 0 ~ 9 출력
```

[ES6 목록으로 가기](https://github.com/Minsoo-web/es_features/blob/master/es6/README.md#-es5-주요-특징들)

## 참고 문서

[정적 타입 언어와 동적 타입 언어](https://inpages.tistory.com/95)  
[변수의 유효 범위](https://victorydntmd.tistory.com/45)
