### ValueError: The truth value of a Series is ambiguous. Use a.empty, a.bool(), a.item(), a.any() or a.all()

if 조건문 이상 없는것 같은데,,, 구글링 해보니 다들

#### 1. and 대신 &, or 대신 | 를 써라 -> 이미 함 
#### 2. () 써라 -> 이미 함
#### 3.  파이썬 연산으로 판다스 df 를 연산하려고 해서 그렇다고 함.

    TRUE FALSE 가 명확하게 바꿔줘야한다고 한다..

 

#### 4. 시리즈 문제
OKKY 질문 답변 인용

if 문에서 숫자랑 비교해서 나온게 Series object 라 참/거짓 value 가 ambiguous 해서 그러니 any, all 같은 Series 의 메소드를 써서 처리해야 합니다. 
Python Pandas Series 같은데 https://pandas.pydata.org/docs/reference/api/pandas.Series.html  참조하세요
 

프로젝트가 너무나 바쁜 나는 이 에러를 뒷전으로 미루고 

친근한 

data.loc 으로 쓰기로 했다. 조건문이 아닌 판다스에 익숙한 요놈으로 해주니 에러 해결!


data.loc[data['okt_score'] < 0, 'okt_score'] = -0.5
data.loc[data['okt_score'] >= 0, 'okt_score'] = 0.5
data.loc[data['okt_score_shop'] < 0, 'okt_score_shop'] = -0.5
data.loc[data['okt_score_shop'] >= 0, 'okt_score_shop'] = 0.5

- 2) A & B 면 C=1 이런식으로 안쓰고 따로 분리해서 A+B의 합산이 4가 넘으면 1 이런식으로 컬럼 연산을 단순화 시키니까 더 빨리 해결 되었다. 
- Pandas는 and or 붙으면 싫어하나보다.. 추후 메꾸기
```python
data['both']=data['okt_score']+data['okt_score_shop']
data['both'].unique()
data['both'].value_counts()
```
