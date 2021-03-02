## 3장 DOM 객체 다루기\_끝말잇기 게임

### 게임 순서

1. 참여자 수 선택

2. 참여자 순서 결정

3. 첫번째 참여자 단어 제시

4. 다음 참여자 단어 제시

5. 참여자 단어 비교

6. 올바르면 다음 참여자가 단어 제시

7. 올바르지 않다면 틀렸음을 표시

8. 게임 계속 진행
   ​

### 사용자에게 표시할 메시지

```js
// 브라우저에 팝업창 생성
prompt("값을 입력하세요", "기본값"); // 값을 입력할 수 있으며, 입력한 값을 반환
confirm("이게 맞나요?"); // 확인과 취소 버튼이 있고, 확인과 취소는 true와 false를 반환
alert("경고!!"); // 흔히 경고창으로 사용하고, 확인버튼이 하나 생기며, 클릭시 undefined를 반환
```

### HTML 태크 선택

```js
document.querySelector("선택자");
document.querySelector("#아이디");
document.querySelector("클레스");
```

### 태그에 이벤트 추가

```js
태그.addEventListener("이벤트 이름", 리스너함수);

const 리스너함수 = (event) => {
  event.target; // 이벤트가 발생한 대상 태그
  event.target.value; // 이벤트가 발생한 대상 태그의 값
  event.target.textContent; // 이벤트가 발생한 대상 태그의 내부 문자
  event.target.focus; // 이벤트가 발생한 대상 태그 하이라이트
};
```

### 순서도 최적화

- 여러 개의 if문을 하나로 합칠때 or(||)인지 and(&&)인지에 따라 진리표가 달라짐

#### OR

| 첫 번째 조건 | 두 번째 조건 | 최종 결과 |
| ------------ | ------------ | --------- |
| true         | true         | true      |
| true         | false        | true      |
| false        | true         | true      |
| false        | false        | false     |

#### AND

| 첫 번째 조건 | 두 번째 조건 | 최종 결과 |
| ------------ | ------------ | --------- |
| true         | true         | true      |
| true         | false        | false     |
| false        | true         | false     |
| false        | false        | false     |

### 코드 작성

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>끝말잇기</title>
  </head>

  <body>
    <div><span id="order">1</span>번째 참가자</div>
    <div>제시어: <span id="word"></span></div>
    <input type="text" />
    <button>입력</button>

    <!-- 스크립트 작성 -->
    <script>
      // 브라우저에 팝업창 표시 후 입력된 값을 변수에 저장
      const number = Number(prompt("몇 명이 참가하나요?"));

      // html 태그 선택
      const $button = document.querySelector("button");
      const $input = document.querySelector("input");
      const $word = document.querySelector("#word");
      const $order = document.querySelector("#order");
      let word; // 제시어
      let newWord; // 현재 단어

      // 버튼 클릭 이벤트 발생 시 동작할 동작문 작성.
      const onClickButton = () => {
        // 제시어가 비어있는지?
        if (!word) {
          word = newWord; // 그 단어가 제시어가 된다.
          $word.textContent = word; // 화면에 제시어 표시
          const order = Number($order.textContent);
          if (order + 1 > number) {
            $order.textContent = 1;
          } else {
            $order.textContent = order + 1;
          }
          $input.value = "";
          $input.focus();
        } else {
          // 비어있지 않다.
          // 단어가 올바른지?
          if (word[word.length - 1] === newWord[0]) {
            // 올바를 경우
            word = newWord; // 현재 단어를 제시어에 저장한다.
            $word.textContent = word; // 화면에 제시어 표시
            const order = Number($order.textContent);
            if (order + 1 > number) {
              $order.textContent = 1;
            } else {
              $order.textContent = order + 1;
            }
            $input.value = "";
            $input.focus();
          } else {
            // 올바르지 않을 경우
            alert("올바르지 않은 단어입니다!");
            $input.value = "";
            $input.focus();
          }
        }
      };
      const onInput = (event) => {
        newWord = event.target.value; // 입력하는 단어를 현재 단어로
      };

      // 작성한 함수를 이벤트가 발생할 때 실행될 수 있도록 이벤트에 연결
      $button.addEventListener("click", onClickButton);
      $input.addEventListener("input", onInput);
    </script>
  </body>
</html>
```
