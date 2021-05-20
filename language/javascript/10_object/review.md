# 객체

## 1. 객체란?

Object <-> Subject

Object

- Subject가 인지하는 모든 것
- 인식가능해야 한다.
- 속성(특징)으로 구분된다.

## 2. 추상화

## 3. class 타입 객체지향 vs. prototype 타입 객체 지향

## 4. Array & Hash Table

- Array: 데이터의 순서로 데이터에 접근할 것이냐
- Hash Tble: 데이터의 이름으로 데이터에 접근할 것이냐

## 5. 프로퍼티 키

- 프로퍼티 키는 식별자 역할을 하지만 식별자는 아니다.

## 6. 유사배열객체

- 프로퍼티 키가 숫자이고 length 프로퍼티를 가지는 객체를 유사배열객체라 한다.

## 7. 회소배열 ~ delete

## 8. 계산된 프로퍼티 키

## 발표주제: [] notation

[] notation

1. 프로퍼티 접근 연산자(property accessor)
1. array literal
1. 객체 프로퍼티 키 연산자(property key operator)

이 역시 함수 리터럴과 같이(함수 선언문, 함수 표현식) 중의적인 리터럴 및 연산자이지만 자바스크립트 엔진에 의해 암묵적으로 해석된다.

### 2. 프로퍼티 접근 연산자(property accessor)

```javascript
1['']; // undefined
1.name; // SyntaxError: Invalid or unexpected token -> 실수표현이므로(context)
(1).name; // undefined
Number(1).name; // undefined
'name'.name; // undefined
```

### 3. 객체 프로퍼티 키 연산자(property key operator)

```javascript
const obj = {
    `one`: 1 // SyntaxError: Unexpected template string
};

console.log(obj);
```

`one` !== 'one'

```javascript
let a = 0;

let obj = {
  `expression-${++a}`: a,
  `expression-${++a}`: a,
  `expression-${++a}`: a
};

obj = {
  [`expression-${++a}`]: a,
  [`expression-${++a}`]: a,
  [`expression-${++a}`]: a
};
```

여기서 obj의 키에 쓰인 [.]은 길이가 1인 배열로 보는 것이 아닌 내부의 표현식을 String type의 값으로 변환해주는 연산자이다. 그렇다면 아래의 코드도 작동할까?

```javascript
const b = {String("a"): 1}; // SyntaxError Unexpected token ':'
```

객체의 키는 String 혹은 Symbol 값이 와야한다. 표현식은 올 수 없다.

```javascript
let a = 0;

let obj = {
  `expression-${++a}`: a, // SyntaxError Unexpected token ':'
  `expression-${++a}`: a,
  `expression-${++a}`: a
};
```

위의 코드가 에러가 나는 이유는 `expression-${++a}`이 표현식이기 때문이다. 'expression-1'과 `expression-${1}`은 모두다 string 타입으로 평가되지만 'expression-1'은 원시값인 반면 `expression-${1}`은 표현식이다.

따라서, 객체 프로퍼티 키 연산자 `[...]`는 표현식이 아닌 값 자체이다.
