# Peak-Finder

주식/선물 시장의 고점을 예측하는 프로젝트입니다.

---

## 전제

    전제 a-1 : 선물 시장 참여자는, 인간이 대다수이다
    전제 a-2 : 대다수의 인간은 비합리적인 동물이며, 비합리적인 행동/판단을 한다
    결론 a : 선물 시장 참여자의 대다수는 비합리적인 동물이며, 비합리적인 행동/판단을 한다

    전제 b-1 : 인터넷 커뮤니티에서, 사람들은 일상에서 있었던 자신의 의견을 표현한다.
    전제 b-2 : 선물 시장 참여자들도, 인터넷 커뮤니티를 이용한다.
    결론 b : 선물 시장 참여자들은 인터넷 커뮤니티에서, 자신의 투자에 대한 의견을 표현한다.

    전제 c : 선물시장은 제로섬 게임이다. 손실을 보는 사람이 있다면, 이득을 보는 사람도 존재한다.

    전제 d : 선물시장의 움직임은 주식시장의 움직임과 비교적 동일하다

## 가설 및 추론

    가설 d-1 : 인간은 선물 시장에서 비합리적인 판단을 한다.
    가설 d-2 : 비합리적인 판단에서 손실이 발생하는 경우가 존재한다.
    추론 d : 인간의 비합리적인 판단 때문에 손실이 발생하는 경우가 존재한다.

    결론 b : 선물 시장 참여자들은 인터넷 커뮤니티에서, 자신의 투자에 대한 의견을 표현한다.
    결론 a : 선물 시장 참여자의 대다수는 비합리적인 동물이며, 비합리적인 행동/판단을 한다.
    추론 e : 선물 시장 참여자들은, 비합리적인 행동/판단을 인터넷 커뮤니티에서 표현할 것이다.

## 가설과 추론에 따른 프로젝트의 프로세스
1. 비합리적인 행동/판단의 표현을 인터넷 커뮤니티에서 수집한다.
2. 오를 것이라고 잘못 판단한 표현이 무엇인지 분석한다.
3. 잘못 판단한 표현이 나온 시점을 근거로 그래프가 꺾이는 지점, 고점을 예측한다

---

# Content

### 1. 데이터 수집

### 2. 전처리

### 3. 자연어처리

### 4. 예측 모델

---

# 1. 데이터 수집

- 방법 : 커뮤니티 작성글/댓글 크롤링
- 사용 라이브러리 : [DC-Crawler](https://github.com/Kain7f1/DC-Crawler)
- 커뮤니티 : dcinside
- 데이터 : 24개의 기업에 대한 검색결과 게시글/댓글 text
- 데이터 수 : 1,153,474 개

---

# 2. 데이터 전처리

## 2-a. 데이터 정제
## 2-b. text 띄어쓰기 적용
## 2-c. 단어 추출
## 2-d. 토큰화
## 2-e. 토큰 데이터 정규화

---

## Contacts

### 이슈 관련
* https://github.com/Kain7f1/Peak-Finder/issues

### E-mail
* kain7f1@gmail.com

---

## License

`DC-Crawler`는 `MIT License` 라이선스 하에 공개되어 있습니다. 모델 및 코드를 사용할 경우 라이선스 내용을 준수해주세요. 라이선스 전문은 `LICENSE` 파일에서 확인하실 수 있습니다.
