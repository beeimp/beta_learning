# 12장 SQL을 이용한 데이터 분석 프로젝트

## 1. 학습 날짜

- 2021년 8월 1일

## 2. 학습진도

- 12장 SQL을 이용한 데이터 분석 프로젝트

## 3. 학습내용

### 1) 코로나 데이터 분석하기

- 일반적인 데이터 분석 과정 - **데이터 수집 -> 데이터 정제 -> 데이터 분석**

1. 데이터 수집하기

   - 코로나 데이터는 [OWID(Our World In Date)](https://github.com/owid/covid-19-data/tree/master/public/data)에서 제공하는 데이터 사용 (책에서는 CSV 파일 사용)

     ```sql
     USE mywork;

     -- 국가 정보 테이블
     CREATE TABLE covid19_country(
         country_code                    VARCHAR(10) NOT NULL,   -- 국가 코드
         country_name                    VARCHAR(80) NOT NULL,   -- 국가명
         countinent                      VARCHAR(50),            -- 대륙명
         population                      DOUBLE,                 -- 인구
         population_density              DOUBLE,                 -- 인구 밀도
         median_age                      DOUBLE,                 -- 평균 연령
         aged_65_older                   DOUBLE,                 -- 65세 이상 인구 비율
         aged_70_older                   DOUBLE,                 -- 70세 이상 인구 비율
         hostpital_beds_per_thousand     INT,                    -- 1000명당 병실 침대수
         PRIMARY KEY (countrycode)
     );

     -- 코로나 데이터 테이블
     CREATE TABLE covid19_data(
         country_code                    VARCHAR(10) NOT NULL,   -- 국가 코드
         issue_date                      DATE        NOT NULL,   -- 발생일
         cases                           INT,                    -- 확진자 수
         new_cases_per_million           DOUBLE,                 -- 100만 명당 확진자 수
         deaths                          INT,                    -- 사망자 수
         icu_patients                    INT,                    -- 중환자 수
         hosp_patients                   INT,                    -- 병원 입원 환자 수
         tests                           INT,                    -- 검사자 수
         reproduction_rate               DOUBLE,                 -- 감염 재생산 지수
         new_vaccinations                INT,                    -- 백신 접종자 수
         stringency_index                DOUBLE,                 -- 방역 지수 (0~100으로 100이 가장 방역 지수 높음)
         PRIMARY KEY (country_code, issue_date)
     );
     ```

   - 데이터 추가

     ```sql
     -- covid19_country INSERT 
     INSERT INTO covid19_country VALUES 
     ('AFG','Afghanistan','Asia',38928341,54.422,18.6,2.581,1.337,0.5),
     ('AGO','Angola','Africa',32866268,23.89,16.8,2.405,1.362,null),
     ('AIA','Anguilla','North America',15002,null,null,null,null,null),
     ('ALB','Albania','Europe',2877800,104.871,38,13.188,8.643,2.9),
     ('AND','Andorra','Europe',77265,163.755,null,null,null,null),
     ('ARE','United Arab Emirates','Asia',9890400,112.442,34,1.144,0.526,1.2),
     ...;

     -- covid19_data INSERT 
     INSERT INTO covid19_data VALUES 
     ('ALB','2020-04-11',17,5.907,0,null,null,'259',0.94,null,84.26),
     ('ALB','2020-04-12',13,4.517,0,null,null,'233',0.96,null,84.26),
     ('ALB','2020-04-13',21,7.297,0,null,null,'193',1,null,84.26),
     ('ALB','2020-04-14',8,2.78,1,null,null,'236',1.01,null,84.26),
     ('ALB','2020-04-15',19,6.602,1,null,null,'252',1.06,null,84.26),
     ...;
     ```

   - 데이터 확인

     ```sql
     SELECT COUNT(*)
     FROM covid19_country;

     SELECT COUNT(*)
     FROM covid19_data;
     ```

2. 데이터 정제하기
    - 데이터 클렌징(Data Cleansing)이라고도 함
    - 데이터 분석을 위해 좋지 않은 데이터를 걸러내는 과정
    1. 불필요한 데이터 삭제하기
        - 중복 집계된 데이터를 삭제

        ```sql
        -- 집계 수가 2배가 될 수 있으니 OWID에서 집계한 데이터 삭제

        DELETE FROM covid19_country
        WHERE country_code LIKE "OWID%";

        DELETE FROM covid19_data
        WHERE country_code LIKE "OWID%";
        ```

    2. 숫자형 컬럼 값 NULL 처리하기
        - NULL 값을 어떻게 처리하느냐에 따라 분석 결과가 달라질 수 있음
        - IFNULL() 함수로 NULL인 경우 0으로 처리할 수 있음
        - but, 번거로우니 데이터에서 NULL을 0으로 변경하기 위해 UPDATE 문 사용함

3. 데이터 분석하기
    - 2020년 사망자 수 상위 10개국 조회하기
    - 2020년 인구 대비 사망자 비율 조회하기
    - 우리나라의 월별 확진자 수와 사망자 수 조회하기
    - 국가별, 월별 확진자 수와 사망자 수 조회하기
    - 우리나의 월별 누적 확진자 수와 사망자 수 조회하기
    - 대륙별 사망자 수 상위 3 개국 조회하기

### 2. 타이타닉 데이터 분석하기

1. 데이터 수집하기
    - [타이나틱 데이터](https://www.kaggle.com/c/titanic/data?select=train.csv)
2. 데이터 정제하기
    - 값의 코드를 보기 쉽게 변경
3. 데이터 수집하기
    - 성별 생존자 수와 사망자 수의 비율 조회하기
    - 연령대별 생존사 수와 삼아자 수의 비율 조회하기
    - 가족 동반과 미동반 시 생존자 수와 사망자 수의 비율 조회하기

### 3. 데이터 시각화하기

- 아파치 제플린(Apache Zeppelin)
  - 노트북 형태로 데이터를 시각화하는 도구
    - 주피터 노트북과 유사
  - SQL문을 실행한 결과를 다양한 형태의 그래프로 보여줌
  - 자바 JDK 필요

## 4. 새롭게 알게된 사실(신선했던 것, 유용했던 점)

- 데이터 분석에 SQL 기능 중 조인, 집계쿼리, 서브쿼리, 윈도우 함수가 자주 사용된다는 것을 예제를 통해 이해할 수 있었습니다.
- 아파치 제플린과 같은 SQL을 통해 시각화할 수 있는 좋은 도구를 알 수 있어 좋았습니다.

## 5. 학습 리뷰

- 책을 끝까지 리뷰하면서 공부할 수 있어서 정말 좋았습니다. 감사합니다!
