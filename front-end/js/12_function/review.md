# 함수

## 함수의 변수 실행 시점: 호출 시

## 인수는 매개변수에 할당되는 표현식 및 값

## 리턴문이 없는 함수를 void라 한다

## 매개변수는 var 변수로 봐도 무방하다

undefined로 초기화되므로

```javascript
function add(x, y) ~ function add(var x, var y)
```

## 순수함수 vs. 비순수함수

- 순수함수
  - 동일한 인수는 동일한 결과를 반환한다.
  - 외부 상태에 의존하지 않고 외부 상태를 변경하지 않는다.
- 비순수함수: 테스트가 곤란하다.

## 고차함수

- 함수의 외부에서 콜백함수를 전달받거나
- 함수를 반환하는 함수

## 비동기 함수

```javascript
setTimeout(function () {
  console.log('Hello');
}, 1000);
```

## 렉시컬 환경 ~ 실행 컨텍스트

## 식별자 resolution
