---
title: 배열 (Array)
categories: JavaScript
author: Bernese-Corgi
---

# 배열

배열은 전역 객체로, 배열을 생성할 때 사용하는 리스트 형태의 고수준 객체이다.

자바스크립트 배열의 타입은 object이다.
```js
const arr = [];

console.log(typeof arr); // object
```

배열은 프로토타입으로 탐색과 변형 작업을 수행하는 메서드를 가진다.
  ⎡ 배열의 생성자 함수 : Array
  ⎣ 배열의 프로토타입 객체 : Array.prototype

```js
// Array : 배열의 생성자 함수
console.log(arr.constructor); // [Function: Array]

// Array.prototype : 배열의 프로토타입 객체
console.log(Object.getPrototypeof(arr) === Array.prototype); // true
```

자바스크립트에서 배열의 길이와 요소의 자료형은 고정되어 있지 않다.

## 희소 배열

배열의 요소가 연속적으로 위치하지 않고 일부가 비어 있는 배열

```js
const sparse = [, 2, , 4];
```

- 자바스크립트는 희소 배열을 문법적으로 허용한다.
- 희소 배열의 length는 희소 배열의 실제 요소 개수보다 언제나 크다.
   ```js
   // length
   console.log(sparse.length); // 4
   // 
   console.log(sparse); // [ <1 empty item>, 2, <1 empty item>, 4 ]
   ```
- 희소배열의 비어 있는 부분은 요소가 존재하지 않는다.
   ```js
   console.log(Object.getOwnPropertyDescriptors(sparse));
   /*
   {
     '1': { value: 2, writable: true, enumerable: true, configurable: true },
     '3': { value: 4, writable: true, enumerable: true, configurable: true },
     length: { value: 4, writable: true, enumerable: false, configurable: false }
   }
   */
   ```
- 희소 배열을 생성하지 않도록 주의해야 한다.
  - 의도적으로 희소 배열을 만들어야 하는 상황은 발생하지 않는다.
  - 희소 배열은 연속적인 값의 집합이라는 배열의 기본적인 개념과 맞지 않는다.
  - 성능에 악영향을 준다.

## 배열 요소 참조

### 인덱스

• 인덱스는 객체의 프로퍼티 키와 같은 역할을 한다. ⇒ 인덱스로 값을 참조할 수 있다

• 자바스크립트의 배열의 인덱스는 0부터 시작한다.
⎡ 첫 번째 요소의 인덱스 = `0`
⎣ 마지막 요소의 인덱스 = `length - 1`

• 인덱스는 문자열을 사용할 수 없고, 정수만 허용한다.

### 요소


### 요소 접근

1. <span style="color: #495F85; font-weight: 700">배열의 요소에 접근할 때는 대괄호 표기법을 사용한다</span>
   • `배열리터럴or배열이름[접근할 인덱스]`
   • 대괄호 안에 인덱스를 입력한다.

   ```js
   const fruits = ['apple', 'banana', 'orange'];

   fruits[0]; // 'apple'
   fruits[1]; // 'banana'
   ```
    <span style="color: gray">왜 대괄호 표기법을 사용해야 할까?</span>
    자바스크립트 배열의 요소는 프로퍼티의 값 역할을 한다.

    <img src="https://user-images.githubusercontent.com/72931773/122608079-95283e80-d0b6-11eb-8ea7-a17748b098fc.png" width="40%" style="margin-left: auto; margin-right: auto; display: block"/>

    프로퍼티 키 인덱스는 정수만 가능하므로 문자열 접근 방식인 `.`으로 접근하면 문법 에러가 발생한다.

    <img src="https://user-images.githubusercontent.com/72931773/122608105-a5d8b480-d0b6-11eb-8ca0-c331a85a2b77.png" width="60%" style="margin-left: auto; margin-right: auto; display: block"/>

    <br/>

1. <span style="color: #495F85; font-weight: 700">정수로 평가되는 표현식이라면 인덱스 대신 사용할 수 있다.</span>

   ```js
   fruits[10 - 8]; // 'orange'
   ```

    <br/>

1. <span style="color: #495F85; font-weight: 700">존재하지 않거나 잘못된 인덱스를 사용하면 `undefined`를 반환한다.</span>
   배열은 인덱스를 나타내는 문자열을 프로퍼티 키로 갖는 객체라고 볼 수 있다.
   존재하지 않는 프로퍼티에 접근했을 때 undefined를 반환하는 것처럼 배열 또한 존재하지 않는 요소를 참조하면 undefined를 반환한다.

   ```js
   fruits['a']; // undefined
   fruits[4]; // undefined
   ```

   희소 배열의 존재하지 않는 요소를 참조해도 undefined가 반환된다.

   ```js
   const sparse = [1, , 3];
   sparse[1]; // undefined
   ```

## length 프로퍼티

Array 인스턴스의 length 속성은 배열의 길이를 반환한다. (배열의 길이 = 배열의 요소 개수)
  ```js
  const fruits = ['apple', 'banana', 'orange'];
  fruits.length; // 3
  ```

반환값
- 부호 없는 32비트 정수형
- 양의 정수 (0 이상의 정수)
- 2^32^ 미만의 값을 가진다.
- 배열의 최대 인덱스보다 항상 크다.

length 속성에 값을 설정할 경우 배열의 길이를 변경한다.

빈 배열인 경우 0을 반환한다.
```js
[].length // ⇒ 0
```

배열 요소를 추가, 삭제하면 자동으로 업데이트 된다.
```js
const arr = [1,2,3,4,5];
console.log(arr.length); // 5

arr.push(6);
console.log(arr.length); // 6

arr.pop();
console.log(arr.length); // 4
```

length 프로퍼티 값에 임의의 숫자 값을 명시적으로 할당할 수 있다.

① 현재 length 값보다 작은 숫자값을 할당할 때
```js
const arr= [1,2,3,4,5];
arr.length = 3;
console.log(arr); // [ 1, 2, 3 ]
```
할당한 숫자값 만큼 배열이 절단되어 갱신된다.

② 현재 length 값보다 큰 숫자값을 할당할 때

```js
const arr = [1,2,3];
arr.length = 6;
```

length 프로퍼티 값은 변경된다.

```js
console.log(arr.length); // 6
```

실제로 배열의 길이가 늘어나지 않는다.

```js
// empty items는 실제 배열의 요소가 아니다.
console.log(arr); // [ 1, 2, 3, <3 empty items> ]
```

값 없이 비어 잇는 요소를 위해 메모리 공간을 확보하지 않고, 빈 요소를 생성하지 않는다.

```js
console.log(Object.getOwnPropertyDescriptors(arr));
/*
{
  '0': { value: 1, writable: true, enumerable: true, configurable: true },
  '1': { value: 2, writable: true, enumerable: true, configurable: true },
  '2': { value: 3, writable: true, enumerable: true, configurable: true },
  length: { value: 6, writable: true, enumerable: false, configurable: false }
}
*/
```




/---
- 요소를 순회할 수 있다 : 배열은 인덱스와 length를 가지기 때문
  <span style="color: #6989bf">▾ for문으로 순회하기</span>

  ```js
  const fruits = ['apple', 'banana', 'orange'];

  for (let i = 0; i < fruits.length; i++) {
    console.log(fruits[i]); // 'apple', 'banana', 'orange'
  }
  ```

  <span style="color: #6989bf">▾ forEach 메서드로 순회하기</span>

  ```js
  const fruits = ['apple', 'banana', 'orange'];

  fruits.forEach((item, index, array) => console.log(item, index)); // apple 0, banana 1, orange 2
  ```

## 배열 생성

---

## 희소 배열

(희소 배열)
배열의 길이는 언제든 늘어나거나 줄어들 수 있기 때문에 자바스크립트의 배열은 밀집도가 보장되지 않는다.
이를 보완하려면 typed array를 사용할 수 있다. (형식화 배열)

## 배열과 객체의 성능 비교

배열이 일반 객체보다 요소에 접근하는 속도가 빠르다.

1. 배열의 성능
   ```js
   const arrPerf = [];

   console.time('Array Perfomance Test');

   for (let i = 0; i < 10000000; i++) {
    arrPerf[i] = i;
   }

   console.timeEnd('Array Perfomance Test'); // Array Perfomance Test: 313.178ms
   ```
2. 객체의 성능
   ```js
   const objPerf = {};

   console.time('Object Perfomance Test');

   for (let i = 0; i < 10000000; i++) {
     objPerf[i] = i;
   }

   console.timeEnd('Object Perfomance Test'); // Object Perfomance Test: 518.416ms
   ```