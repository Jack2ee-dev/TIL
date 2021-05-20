# 연산자 표현식

- "연산자 표현식도 값으로 평가될 수 있는 표현식이다."이라는 표현이 나오는 데 "값으로 평가되어야야 하는 표현식이다."가 더 적절하지 않을까?
- NaN를 일치 비교 연산자로 비교하면 false가 나오는 이유나 원리는 무엇인가?

- 논리 연산자는 둘 중 하나의 값을 반환한다.
- typeof function은 function으로 나오는 이유?
- typeof undeclared; // -> undefined
- 블록문: 실행 단위, 중괄호로 묶어야만 블록문이다.
- for (; i < 0 ; i++) {}
- +{} = NaN, +[] = 0, +[10, 20] = NaN
- 옵셔널 체이닝 연산자 --> null/undefined --> undefined
- 부수효과를 일으키는 연산자: ++, --, =, delete(프로퍼티 삭제)
- 선언형 프로그래밍이란?

- string, number, boolean에 .을 찍는 순간 wrapper 객체로 싸여진다.

- 동일한 역할을 하는 함수와 연산자 중 연산자를 사용하는 것이 좋다.

## 1. NaN === NaN 표현식이 false로 평가되는 이유?

### 알아야 할 사항

- NaN의 타입
- JS spec: 11.9.6 The Strict Equality Comparison Algorithm

### 분석 결과

1. NaN의 타입

```javascript
console.log(typeof NaN); // number
```

- +: Infinity + (-Infinity)
- \-: 0 \- (Infinity)
- /: (Infinity) / (Infinity)
- REM: X REM 0, (infinity) REM Y
- square root: x < 0; square root of x

1. JS spec

```javascript
x === y

if (typeof x !== typeof y) {
    return false
} else if (typeof x === 'undefined') {
    return true
} else if (x === null) {
    return true
} else if (typeof x === 'number') {
    if (x === NaN) {
        return false
    } else if (y === NaN) {
        return false
    } else if (x === y) {
        return true
    } else if (x === +0 and y === -0) {
        return true
    } else if (x === -0 and y === 0) {
        return true
    } else {
        return false
    }
}...
```
