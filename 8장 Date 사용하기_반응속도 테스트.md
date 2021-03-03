## 8장 Date 사용하기\_반응속도 테스트

### ClassList

```js
태그.classList;
```

- 태그에 붙은 클래스를 조작

#### 클래스 존재 유무 확인

```js
태그.classList.contains("클래스");
```

#### 클래스의 추가/수정/제거

```js
태그.classList.add("클래스"); // 추가
태그.classList.replace("클래스", "수정클래스"); // 수정
태그.classList.remove("클래스"); //제거
```

### Date

```js
new Date(); // 현재 시각 반환
new Date(연, 월, 일, 시, 분, 초); // 인수에 맞는 시각 반환
```

```js
const startDate = new Date(2020, 11, 21); // undefined
const endDate = new Date(2020, 12, 3); //undefined
(endDate - startDate) / 1000 / 60 / 60 / 24; // 13
```

### Reduce

- 배열에 있는 반복 메서드의 일종
- 배열의 모든 요소를 하나의 값으로 합침

```js
배열.reduce((누적값, 현재값) => {
  return 새로운누적값;
}, 초기값);
```
