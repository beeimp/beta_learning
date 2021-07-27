# 6장 SQL 함수 사용하기

## 1. 학습 날짜

- 2020년 7월 26일

## 2. 학습진도

- 6장 SQL 함수 사용하기

## 3. 학습내용

### SQL 함수란

#### 작동 방식

- `SELECT` 문 단독 사용
- `SELECT` 문에 함수를 사용하여 매개변수 전달
- 예시
  ```SQL
  SELECT ABS(1), ABS(-1);
  SELECT LENGTH("mysql");
  ```

#### SQL 함수의 종류

| 함수 종류 | 설명                                      | 해당 함수                |
| --------- | ----------------------------------------- | ------------------------ |
| 숫자형    | 연산 대상과 반환값이 숫자형               | ABS(), ROUND() 등        |
| 문자형    | 연산 대상과 반환값이 문자형               | CONCAT(), SUBSTRING() 등 |
| 날짜형    | 연산 대상과 반환값이 날짜형               | SYSDATE(), YEAR() 등     |
| 형 변환   | 연산 대상과 데이터 타입 변환              | CAST(), CONVERT() 등     |
| 기타      | 흐름을 제어하는 함수                      | IF(), CASE 등            |
| 집계      | 집계 쿼리에서 사용하는 함수               | SUM(), MAX(), AVG() 등   |
| 윈도우    | 좀 더 세밀한 데이터 분서을 위한 분석 함수 | RANK(), LAG() 등         |

### 기본 SQL 함수 살펴보기

#### 수식 연산자

- 숫자를 대상으로 +(더하기), -(빼기), \*(곱하기), /(나누기), % 또는 MOD(나머지), DIV(나누기, 몫을 정수로 변환) 등의 계산하는 연산자

```SQL
SELECT 1+2, 3-4, 5*6, 7/8, 7 DIV 8, 9%10, 9 MOD 10;
```

#### 숫자형 함수

|            함수            |                                                                                     반환값 |
| :------------------------: | -----------------------------------------------------------------------------------------: |
|           ABS(x)           |                                                                                 x의 절댓값 |
|   CEIL(x)<br/>CELING(x)    |                                                                                       올림 |
|          FLOOR(x)          |                                                                                       내림 |
|           EXP(x)           |                                                                              e<sup>x</sup> |
|           LN(x)            |                                                                              자연로그 ln x |
|         LOG(b, x)          |                                                                          log<sub>b</sub> x |
|          LOG10(x)          |                                                                         log<sub>10</sub> x |
|          LOG2(x)           |                                                                          log<sub>2</sub> x |
| POW(x, y)<br/> POWER(x, y) |                                                                              x<SUP>y</SUP> |
|         RAND([n])          |                                0보다 크거나 같고 1보다 작은 실수인 난수<br/> n은 생략 가능 |
|        ROUND(x, d)         | 실수 x를 소수점 이하 d 자리까지 반올림<br/> d 생략시 정수 반환<br/> d가 음수면 기준점 이동 |
|          SIGN(x)           |                                         x가 0보다 크면 1<br/> 0이면 0<br/> 0보다 작으면 -1 |
|          SQRT(x)           |                                                                                   제곱근 x |
|       TRUNCATE(x, d)       |                                                  실수 x를 소수점 이하 d 자리점에서 자른 값 |

#### 문자형 함수

- 문자나 문자열을 대상으로 연산을 수행해 결과값 반환

|                                    함수                                     |                                                                                    반환값 |
| :-------------------------------------------------------------------------: | ----------------------------------------------------------------------------------------: |
|                 CHAR_LENGTH(str),<br/>CHARACTER_LENGTH(str)                 |                                                                    str 문자열의 문자 개수 |
|                                 LENGTH(str)                                 |                                                              str 문자열의 바이트(Byte) 수 |
|                             CONCAT(s1, s2, ...)                             |                                                      여러 문자열을 하나의 문자열로 붙여서 |
|                         CONCAT_WS(sep, s1, s2, ...)                         |                                                여러 문자열을 sep로 연결(조인 함수와 유사) |
|                                FORMAT(x, d)                                 |                      숫자 x의 정수 부분 3자리 마다 콤마 추가 후 소수점 d 자리 기준 반올림 |
|                             INSTR(str, substr)                              |                                          str 문자열에서 substr 문자를 찾아 시작 위치 반환 |
|           LOCATE(substr, str, pos), <BR/>POSITION(substr IN str)            | str 문자열에서 substr 문자를 찾아 시작 위치 반환 <BR/>pos 입력 시 해당 위치부터 검색 시작 |
|                         LOWER(str),<BR/>LCASE(str)                          |                                                                str 문자열을 소문자로 반환 |
|                         UPPER(str),<BR/>UCASE(str)                          |                                                                str 문자열을 대문자로 반환 |
|                           LPAD(str, len, padstr)                            |                    str 문자열을 len 길이만큼 반환하는데, 자리가 남으면 padstr 문자로 채움 |
|                           RPAD(str, len, padstr)                            |             str 문자열을 len 길이만큼 반환하는데, 자리가 남으면 오른쪽 padstr 문자로 채움 |
|                                 LTRIM(str)                                  |                                                             str 문자열에서 왼쪽 공백 제거 |
|                                 RTRIM(str)                                  |                                                           str 문자열에서 오른쪽 공백 제거 |
|             TRIM([{BOTH\|LEADING\|TRAILING} [remstr] FROM] str)             |        str 문자열에서 remstr 문자를 앞(LEADING)이나 뒤(TRAILING) 또는 앞뒤(BOTH)에서 제거 |
|                               LEFT(str, len)                                |                                              str 문자열을 len 길이만큼 왼쪽에서 잘라 반환 |
|                               RIGHT(str, len)                               |                                            str 문자열을 len 길이만큼 오른쪽에서 잘라 반환 |
|                             REPEAT(str, count)                              |                                                               str 문자열을 count만큼 반복 |
|                       REPLACE(str, from_str, to_str)                        |                                       str 문자열에서 from_str 문자열을 찾아 to_str로 변경 |
|                                REVERCE(str)                                 |                                                                  str 문자열을 거꾸로 반환 |
|                                  SPACE(n)                                   |                                                                      n개의 공백 문자 반환 |
| SUBSTR(str, pos, len),<BR/>SUBSTRING(str, pos, len),<BR/>MID(str, pos, len) |                                 str 문자열의 pos 위치에서 len 길이만큼 문자를 잘라서 반환 |
|                             STRCMP (str1, str2)                             |            str1과 str2 문자열을 비교해 같으면 0, str1이 str2보다 크면 1, 작으면 -1을 반환 |

#### 날짜형 함수

|                                   함수                                    |                                       반환값 |
| :-----------------------------------------------------------------------: | -------------------------------------------: |
|              CURDATE(),<BR/>CURRENT_DATE(),<BR/>CURRENT_DATE              |                                    현재 날짜 |
|              CURTIME(),<BR/>CURRENT_TIME(),<BR/>CURRENT_TIME              |                          현재 시작(시:분:초) |
|           NOW(),<BR/>CURRENT_TIMESTAMP(),<BR/>CURRENT_TIMESTAMP           |                             현재 날짜와 시간 |
|                               DAYNAME(date)                               |                                  date의 요일 |
|                      DAYOFMONTH(date),<BR/>DAY(date)                      |                                  date에서 일 |
|                              DAYOFWEEK(date)                              |             date에서 요일별 숫자(1-일, 7-토) |
|                              DAYOFYEAR(date)                              |        date에서 1월 1일부터 일수(1-일, 7-토) |
|                              LAST_DAY(date)                               |                 date가 속한 월의 마지막 날짜 |
|                                YEAR(date)                                 |                                date에서 연도 |
|                                MONTH(date)                                |                                  date에서 월 |
|                               QUARTER(date)                               |                                date에서 분기 |
|                             WEEKOFYEAR(date)                              |                                  date의 주차 |
|                                HOUR(time)                                 |                                time에서 시간 |
|                               MINUTE(time)                                |                                  time에서 분 |
|                               SECOND(time)                                |                                  time에서 초 |
|                                DATE(expr)                                 |                           expr에서 날짜 부분 |
|                                TIME(expr)                                 |                           expr에서 시간 부분 |
| DATE_ADD(date, INTERVAL expr unit),<BR/>ADDDATE(date, INTERVAL expr unit) |                 date에 expr unit을 더한 날짜 |
|                            ADDDATE(expr, days)                            |                      expr에 days를 더한 날짜 |
| DATE_SUB(date, INTERVAL expr unit),<BR/>SUBDATE(date, INTERVAL expr unit) |              date에 expr unit을 뺀 날짜 반환 |
|                            SUBDATE(expr, days)                            |                 expr에서 days를 뺀 날짜 발환 |
|                          EXTRACT(unit FROM date)                          |           date에서 unit으로 지정된 부분 반환 |
|                          DATEDIFF(expr1, expr2)                           |                    expr1에서 expr2를 뺀 날짜 |
|                         DATE_FORMAT(date, format)                         |   date를 format에 명시된 형태로 변환 후 반환 |
|                         STR_TO_DATE(str, format)                          |              str을 format에 맞게 날짜로 변환 |
|                        MAKEDATE(year, day_of_year)                        | year에 day_of_year에 해당하는 일수 더한 날짜 |
|                                 SYSDATE()                                 |                                    현재 날짜 |
|                             WEEK(date, mode)                              |                           date가 몇 주차인지 |
|                           YEARWEEK(date, mode)                            |                      date가 속한 연도와 주차 |

- date은 'YYYY-MM-DD'
- expr은 'YYYY-MM-DD hh-mm-ss'
- days는 숫자(ex - 10)
- unit은 다음과 같음

  | unit value    |      설명      |   expr 형식   |
  | ------------- | :------------: | :-----------: |
  | YEAR          |       연       |      연       |
  | MONTH         |       월       |      월       |
  | QUARTER       |      분기      |     분기      |
  | WEEK          |       주       |      주       |
  | DAY           |       일       |      일       |
  | HOUR          |       시       |      시       |
  | MINUTE        |       분       |      분       |
  | SECOND        |       초       |      초       |
  | YEAR_MONTH    |     년,월      |    '년-월'    |
  | DAY_HOUR      |     일, 시     |    '일 시'    |
  | DAY_MINUTE    |   일, 시, 분   | '일 시:분:초' |
  | DAY_SECOND    | 일, 시, 분, 초 | '일 시:분:초' |
  | HOUR_MINUTE   |     시, 분     |    '시:분'    |
  | HOUR_SECOND   |   시, 분, 초   |  '시:분:초'   |
  | MINUTE_SECOND |     분, 초     |    '분:초'    |

- format은 다음과 같음

| 식별자 |             설명             |
| :----: | :--------------------------: |
|   %Y   |          4자리 연도          |
|   %y   |          2자리 연도          |
|   %M   |        월의 영문 표기        |
|   %m   |           2자리 월           |
|   %b   |     월의 축양 영문 표기      |
|   %c   |          숫자형 월           |
|   %d   |           2자리 일           |
|   %e   |           1자리 일           |
|   %j   |     3자리 1년 기준 일 수     |
|   %H   |        24시간 기준 시        |
| %h, %l |        12시간 기준 시        |
|   %p   |    AM(오전) 또는 PM(오후)    |
|   %i   |           2자리 분           |
| %S, %s |           2자리 초           |
|   %T   |     24시간 기준 시:분:초     |
|   %r   | 12시간 기준 시:분:초 AM\| PM |
|   %W   |       요일의 영문 표기       |
|   %w   |     숫자 요일(0부터 일)      |
|   %U   | 00~53 형식 주차(일부터 시작) |
|   %u   | 00~53 형식 주차(월부터 시작) |
|   %V   | 01~53 형식 주차(일부터 시작) |
|   %v   | 01~53 형식 주차(일부터 시작) |

#### 기타 함수

- 형 변환 함수

  - 데이터 타입을 변환하는 함수

  - CAST(expr AS type)

    - 매개변수 expr 값을 type에 명시한 데이터 타입으로 변환한 결과를 반환하는 함수
      ```sql
      SELECT CAST(매개변수 AS 타입)
      ```

    |      type 값      | 데이터 타입 | 변환 타입 |
    | :---------------: | :---------: | --------: |
    |     CAHR([n])     |   문자형    |      CHAR |
    |      SIGNED       |   숫자형    |    정수형 |
    | DECIMAL[{M[, D]}] |   숫자형    |   DECIMAL |
    |      DOUBLE       |   숫자형    |    DOUBLE |
    |    FLOAT[(p)]     |   숫자형    |     FLOAT |
    |       DATE        |   날짜형    |      DATE |
    |     DATETIME      |   날짜형    |  DATETIME |

  - CONVERT(expr, type)
    - CAST 함수와 달리 AS type 대신 type을 두 번째 매개변수로 받음
      ```sql
      SELECT CONVERT(매개변수, 타입)
      ```

- 흐름 제어 함수

  - 특정 조건을 확인해 조건에 부합하는 경우와 그렇지 않은 경우에 따라 다른 값을 반환하는 함수
  - IF, IFNULL, NULLIF
  - 비슷한 역할인 CASE 연산자가 있음

  - IF(조건식, 참일 경우 반환할 값, 거짓일 경우 반환할 값)
    ```sql
    SELECT IF(조건식, 참일 경우 반환할 값, 거짓일 경우 반환할 값)
    ```
  - IFNULL(해당 값이 NULL이 아닐 경우 반환할 값, 왼쪽 값이 NULL일 경우 반환할 값)
    ```sql
    SELECT IFNULL(해당 값이 NULL이 아닐 경우 반환할 값, 왼쪽 값이 NULL일 경우 반환할 값)
    ```
  - NULLIF(왼쪽 값과 오른쪽 값이 같으면 왼쪽 값 반환, 다르면 오른쪽 값 반환)
  - CASE

    - 함수가 아닌 연산자
    - 흐름 제어 함수와 유사

    ```sql
    -- 방법 1
    CASE value WHEN value와 비교할 값1 THEN 같을 경우 반환할 값
    WHEN value와 비교할 값2 THEN 같을 경우 반환할 값
    ...
    ELSE 모두와 같지 않을 경우 반환할 값

    -- 방법 2
    CASE WHEN 조건1 THEN 조건1이 참일 경우 반환할 값
    WHEN 조건2 THEN 조건2가 참일 경우 반환할 값
    ...
    ELSE 모두 거짓일 경우 반환할 값
    ```

- 기타 함수
  - SLEEP(duration) -잠시 대기하다 0을 반환
  - DATABASE(), SCHEMA(), USER()
    - 각각 데이터베이스 네임, 스키마 네임, 사용자 네임 반환

## 4. 새롭게 알게된 사실(신선했던 것, 유용했던 점)

- SQL의 함수 부분에서 간단한 예시가 잘 정리되어 있어 좋았습니다.

## 5. 학습 리뷰

- 별견 아니지만 196페이지에서 수식 연산자, 숫자형 함수 순으로 설명이 되어 있기 때문에 `6.2.1 숫자형 함수와 수식 연산자`에서 `6.2.1 수식 연산자와 숫자형 함수` 라고 하는건 어떨까요?
