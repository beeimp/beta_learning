## 10장 클래스\_텍스트 RPG 게임 만들기

### JSON.parse, JSON.stringify

#### JSON.parse

- 문자열을 객체로 반환하는 메서드

#### JSON.stringify

- 객체를 문자열로 반환하는 메서드

#### 대상 객체 깊은 복사<sub>deep copy</sub>

```js
const result = JSON.parse(JSON.stringify(객체));
```

### this

- 기본적으로 **window** 객체를 가리킴

### window 객체

- 브라우저가 가리키는 객체
- window 객체 안에는 브라우저가 제공하는 기본 객체와 함수들 있음
- 생략 가능.
  - window.document -> document
  - window.console.log -> console.log

### 클래스

- 객체를 생성하기 위한 템플릿(서식)
- 2015년 자바스크립트에 추가된 문법

#### 공장<sub>factory</sub> 함수

- 객체를 변환하는 함수

```js
function people(name, age, gender) {
  return { name, age, gender };
}
```

#### 생성자<sub>constructor</sub> 함수

- 함수 앞에 **new**를 붙여 호출
- 보통 생성자 함수는 대문자로 시작
- class에서는 클래스를 선언하고, constructor 메서드 안에 객체 주입

### 프로토타입<sub>prototype</sub> 속성

- 생성자 함수에 메서드를 추가할 때 사용
- 프로토타입 메서드 : prototype 속성 안에 추가한 메서드

```js
function People(name, age, gender) {
  return { name, age, gender };

People.prototype.nextYear = function(people){
  this.age += 1;
}
```

### bind 메서드

- this를 수정하게 해주는 내장 메서드
- 화살표 함수는 수정 불가

### 상속

- 여러 클래스에서 공통되는 부분만 추려 만든 새로운 클래스를 여러 클래스에서 가져와 사용하는 것
- extends 예약어 사용
- 상속하는 클래스 - 부모 클래스 / 상속 받는 클래스 - 자식 클래스
