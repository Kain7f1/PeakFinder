# Peak-Finder
- 커뮤니티 반응을 분석하여, 주식의 고점을 예측합니다
- 자연어 처리, 데이터 분석
- [Notion 페이지](https://kain7f1.notion.site/PeakFinder-Short-Term-Highs-4f58a81e104944eea0e9c9c9902a46bf)


#### 전제

    전제 a-1 : 선물 시장 참여자는, 인간이 대다수이다
    전제 a-2 : 대다수의 인간은 비합리적인 동물이며, 비합리적인 행동/판단을 한다
    결론 a : 선물 시장 참여자의 대다수는 비합리적인 동물이며, 비합리적인 행동/판단을 한다

    전제 b-1 : 인터넷 커뮤니티에서, 사람들은 일상에서 있었던 자신의 의견을 표현한다.
    전제 b-2 : 선물 시장 참여자들도, 인터넷 커뮤니티를 이용한다.
    결론 b : 선물 시장 참여자들은 인터넷 커뮤니티에서, 자신의 투자에 대한 의견을 표현한다.

    전제 c : 선물시장은 제로섬 게임이다. 손실을 보는 사람이 있다면, 이득을 보는 사람도 존재한다.

    전제 d : 선물시장의 움직임은 주식시장의 움직임과 비교적 동일하다

### 가설 및 추론

    가설 d-1 : 인간은 선물 시장에서 비합리적인 판단을 한다.
    가설 d-2 : 비합리적인 판단에서 손실이 발생하는 경우가 존재한다.
    추론 d : 인간의 비합리적인 판단 때문에 손실이 발생하는 경우가 존재한다.

    결론 b : 선물 시장 참여자들은 인터넷 커뮤니티에서, 자신의 투자에 대한 의견을 표현한다.
    결론 a : 선물 시장 참여자의 대다수는 비합리적인 동물이며, 비합리적인 행동/판단을 한다.
    추론 e : 선물 시장 참여자들은, 비합리적인 행동/판단을 인터넷 커뮤니티에서 표현할 것이다.

### 가설과 추론에 따른 프로젝트의 프로세스
1. 비합리적인 행동/판단의 표현을 인터넷 커뮤니티에서 수집한다.
2. 오를 것이라고 잘못 판단한 표현이 무엇인지 분석한다.
3. 잘못 판단한 표현이 나온 시점을 근거로 그래프가 꺾이는 지점, 고점을 예측한다


---

## Content
### 1. 기업 선정
### 2. 텍스트 수집
### 3. 텍스트 전처리
### 4. 예측 모델

---

## 1. 기업 선정

> 조건 1: 선물 가능한 주식  
> 조건 2 : 데이터가 많은 기업   
> 조건 3 : 심리적 영향으로 주가가 급등/급락한 기업
- 선정된 기업 : 24개
  - 에코프로, 엘앤에프, LG화학, 피엔티, 금양, LG에너지솔루션
  - 에스엠, 하이브, jyp, 카카오
  - 코스맥스, 아모레, 한국콜마, 휴젤
  - 현대차, 기아
  - 넷마블, 컴투스, 펄어비스, 엔씨소프트
  - 셀트리온, 이마트, 안랩, SK하이닉스

---

## 2. 텍스트 수집


- 방법 : 웹 크롤링 - 커뮤니티 작성글/댓글
- 커뮤니티 : dcinside
- 수집한 데이터 : 24개의 기업에 대한 검색결과 게시글/댓글 text
- 데이터 수 : 1,153,474 개
- 사용 라이브러리 : [DC-Crawler](https://github.com/Kain7f1/DC-Crawler)

---

## 3. 텍스트 전처리

> ### 3-a) 데이터 정제

#### 3-a-0. 우리 프로젝트의 목적
  - 투자자의 “감정”을 읽는 것이 주 목적이다.
  - 그러므로 숫자와 대부분의 특수문자는 무의미하다
  - 한글 감정 표현을 잡아내는 것이 주 목적이다

#### 3-a-1. 정제 계획
  - 특수문자 : !, ? 를 제외하고 전부 공백 문자로 치환한다
  - 숫자 : 공백 문자로 치환
  - 영어 : 모든 알파벳을 소문자로 바꾼다

#### 3-a-2. 정제 진행
  - 한글, 영어, '!', '?'만 남기고 전부 공백문자로 치환한다.
  - 공백 문자가 연속적으로 있는 걸 1개로 줄인다
  - 연속되는 '!', '?' 를 최대 1개로 줄임
  - 연속되는 한글 자음, 모음을 최대 3개로 줄임

#### 3-a-3. 함수화
  - .csv 파일의 경로만 지정하면 모든 과정을 수행할 수 있도록 함수화한다.

> ### 3-b) 띄어쓰기

#### 3-b-0. 띄어쓰기를 하는 이유
  - 커뮤니티 text는 띄어쓰기가 잘 되어있지 않다
  - 원활한 word extraction을 위해 띄어쓰기를 해주어 단어의 경계를 그어준다
  - 사용할 라이브러리 : soynlp
      - 모든 text를 원하는 대로 띄어쓰기 해주는 것은 아니다.
      - 하지만 원하지 않는 방향으로 띄어쓰기 하는 일은 거의 없다
      - 다음 공정에 조금이라도 도움을 주기 위한 프로세스이다.

#### 3-b-1. 띄어쓰기 계획
  1. text로만 이루어진 txt 파일 만들기
  2. spacing 모델 학습
  3. spacing 모델을 파일로 저장한다
  4. 함수화
      1. spacing 모델을 불러온다
      2. 기존의 파일에 적용한다 
      3. 새로운 파일을 만든다

> ### 3-c) 단어 추출

#### 3-c-0.단어 추출을 하는 이유
  - 커뮤니티 text는 신조어, 은어가 많다.
  - 토큰화를 하기 위해선, 신조어와 은어를 추출해야 한다.

#### 3-c-1. 단어 추출 계획
  - text로만 이루어진 txt 파일 만들기
  - soynlp 의 WordExtractor 를 이용하여 단어 추출


> ### 3-d) 토큰화

#### 3-d-1. 토큰화 계획
  - word extraction 한 단어 리스트로 사용자 정의 사전을 만든다
  - mecab 이용하여 tokenizing 한다

#### 3-d-2. 사용자 정의사전 만들기

````
1. mecab 을 컴파일한다
    1. 테스트할 text 를 제작한다
    2. 토큰화 테스트
2. word extraction의 결과 단어 리스트를 불러온다
3. 사용자 정의 사전을 제작하고, .csv 파일로 저장해둔다
    1. 종성이 있는지 판단한다
4. 여기까지 함수화한다 (단어 리스트 불러오기 + 사용자 정의 사전 파일로 저장)
5. 사용자 정의 사전을 `**C:\mecab\user-dic**` 에 옮긴다
6. 사용자 정의 사전을 컴파일한다
````

#### 3-d-3. 토큰화 프로세스

##### 1. 테스트
   1. 안랩 데이터로 테스트를 진행하였다
   2. 테스트 결과
      - ['안랩', '못사', '서', '벼락', '자지', '됐', '지만', '안철수', '가', '답', '이', '다', '그리고', '슨', '피', '는', '신', '이', '지', '오늘', '더', '넣', '을', '거', '야', '씨발', '들', '아', '!']

##### 2. 토큰화 방법
   1. 품사를 기준으로 걸러내기
     - ['NNG', 'NNP', 'NNB', 'VV', 'VA', 'MM', 'MAG', 'MAJ', 'IC', 'SF', 'SY']
     - 품사가 합성된 단어의 경우, 첫번째 품사를 기준으로 한다
     - 결과
       - ['안랩', '못사', '벼락', '자지', '안철수', '답', '그리고', '슨', '피', '신', '오늘', '더', '넣', '거', '씨발', '들', '!']
   2. 1글자 버리기 (!, ? 제외)
     - 1글자 토큰은 무의미한 경우가 많다
     - 결과
       - ['안랩', '못사', '벼락', '자지', '안철수', '그리고', '오늘', '씨발', '!']

##### 3. 함수화  
````python
tokens = tokenize_text(input_text)
print(tokens)
````        
        
##### 4. 원본 text 파일에 적용하여 저장
   - “tokens” 칼럼을 생성한다
   - 각 요소는 토큰들의 list 형태로 저장 
      ```python
      # 사용 예시
      fpath_to_read = "2_spaced_annlab_text.csv"
      text_column_name = "spaced_text"
      fpath_to_save = "4_tokenized_annlab_text.csv"
          
      # 토큰화된 파일 만들기
      make_tokenized_csv_file(fpath_to_read, text_column_name, fpath_to_save)
      ```

#### 3-d-x. 토큰화 Issue/Blocker
- 품사를 기준으로 나누려고 했는데, 품사가 섞어있는 경우
    - ex) 놓쳐서	VV+EC,*,F,놓쳐서,Inflect,VV,EC,놓치/VV/*+어서/EC/*
    - 이 경우 품사가 “VV+EC” 여서 첫번째 품사인 VV를 기준으로 하기로 결정하였다

---

## 4. 데이터 분석

### 4-a. 안랩 데이터 분석

![Ahnlab_analysis.png](image_files%2FAhnlab_analysis.png)

> 2022-03-18 ~ 03-25
- Peak를 찍은 날짜 : 2022-03-23
- 2022-03-24 에 폭락하였다
- 21일까지 잠잠하다
- 22일에 살짝 주목받는다
- 23일에 관심이 터진다
    - 22일에는 조용했던 키워드 언급량이 폭증함
- 24일 버블붕괴
    - "새끼", “병신” 빈도 증가
- 실제 차트  
![Ahnlab_chart.png](image_files%2FAhnlab_chart.png)


### 4-b. 에코프로 데이터 분석
#### 4-b-1) 전체 데이터 시각화 
![ecopro_tokens.png](image_files%2Fecopro_tokens.png)

> 전체 데이터 : 토큰 빈도순으로 시각화

#### 4-b-2) 2023-07-20 ~ 07-28 데이터 분석 
![ecopro_peak_tokens_1.png](image_files%2Fecopro_peak_tokens_1.png)
![ecopro_peak_tokens_2.png](image_files%2Fecopro_peak_tokens_2.png)

> 2023-07-20 ~ 07-28 토큰 언급량 추이 시각화 

---

### Contacts

#### 이슈 관련
* https://github.com/Kain7f1/Peak-Finder/issues

#### E-mail
* kain7f1@gmail.com

---

### License

`DC-Crawler`는 `MIT License` 라이선스 하에 공개되어 있습니다. 모델 및 코드를 사용할 경우 라이선스 내용을 준수해주세요. 라이선스 전문은 `LICENSE` 파일에서 확인하실 수 있습니다.
