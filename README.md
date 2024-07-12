<div align="center">
    <img src="https://capsule-render.vercel.app/api?type=waving&color=FF0000&height=240&text=SKN01-2nd-1Team&animation=&fontColor=ffffff&fontSize=90" />
</div>

# :bow_and_arrow:SKN01-2nd-1Team
Vue + Django + FastAPI 기반 가입 고객 이탈 예측 및 구매 동향 예측

SK 네트웍스 Family AI 캠프 과정 2차 단위 프로젝트

## WBS를 Agile Board(애자일 보드) 로 변경

```c
실제로 우리는 수업 초반부터 프로세스를 학습하여
과정 전반에 걸쳐 애자일 프로세스를 사용하며 Backlog를 작성하고 있습니다.
그러므로 폭포수 방식의 WBS 보다는 저희가 사용하는 애자일 프로세스에 맞게
애자일 보드의 Status View와 Domain View를 위주로 업로드하기로 하였습니다.
```

# 1. 팀 소개
<table align=center>
  <tbody>
    <tr>
      <td align="center">
        <div>
          <img src="https://github.com/user-attachments/assets/4d97616d-34b6-4495-aa18-dc1bb2733d4a"width="100px;"height="100px;" alt=""/>
          <a href="https://github.com/JUNGUIHEON"><div align=center>팀장 정의헌</div></a>
        </div>
      </td>
      <td align="center">
        <div>
          <img src="https://github.com/user-attachments/assets/7712ae53-2ac4-4c1a-9357-73709de29243"width="100px;" alt=""/>
          <a href="https://github.com/gigcot"><div align=center>이재호</div></a>
        </div>
      </td>
      <td align="center">
        <img src="https://github.com/user-attachments/assets/7cbbcc77-39de-4dc6-be12-a2879ce15a0b"width="100px;" alt=""/>
        <a href="https://github.com/JUNGUIHEON"><div align=center>임영훈</div></a>
      </td>
      <td align="center">
        <img src="https://github.com/user-attachments/assets/77eff59b-1c54-4d91-a49c-5f81cf28fb35"width="100px;" alt=""/>
        <a href="https://github.com/JUNGUIHEON"><div align=center>최인헌</div></a>
      </td>
      <td align="center">
        <img src="https://github.com/user-attachments/assets/c1ad2b33-3e67-4dcc-8240-ec3e3665ac61"width="100px;" alt=""/>
        <a href="https://github.com/JUNGUIHEON"><div align=center>허우영</div></a>
      </td>
    </tr>
  </tbody>
</table>

# 2. 프로젝트 개요
- 프로젝트 명: Waiting
- 프로젝트 소개: 모든 OTT의 독점 서비스를 Waiting에서 전부 사용 가능하다!
- 프로젝트 필요성(배경): OTT 서비스를 한 눈에 볼 수 없어서 여러 서비스 사이트에서 구독을 해야 하는데 이걸 하나로 이용할 수 없을까 ? 에서 시작 되었습니다.
- 프로젝트 목표: OTT 서비스 가입 고객들의 이탈률 예측 및 OTT 서비스 구현

# 3. 가설과 가설 검정

### :heavy_check_mark:가설 1: 고객의 가입 기간이 길수록 이탈 가능성이 낮다
- **데이터 수집**: 고객 가입 기간과 이탈 여부 데이터 수집
- **통계 분석**: 가입 기간과 이탈 여부 간의 상관 관계 분석
- **결과 해석**: 유의미한 상관 관계가 있는지 확인

### :heavy_check_mark:가설 2: 특정 상품을 자주 구매한 고객은 다른 유사한 상품도 구매할 가능성이 높다
- **데이터 수집**: 고객의 상품 구매 이력 데이터 수집
- **통계 분석**: 특정 상품과 유사한 다른 상품 구매 빈도 간의 상관 관계 분석
- **결과 해석**: 유사한 상품 구매 패턴이 존재하는지 확인

# 4. 수행결과(테스트/시연 영상)
<div align=left><h2>:movie_camera:발표 영상</div>
  <div align=center>
    <img src="https://github.com/user-attachments/assets/dd04dd05-7f47-4001-936c-12c469b7d1e2"width="800px">
    <a href="https://www.youtube.com/watch?v=Mcd3E41yM1c"><div>영상 보러가기</div></a>
  </div>

## 분석을 위한 전처리 코드
```c
import pandas as pd
from sklearn.preprocessing import LabelEncoder, StandardScaler

# 데이터 로드
members_df = pd.read_excel('./generated_members.xlsx')
orders_df = pd.read_excel('./generated_orders.xlsx')
returns_df = pd.read_excel('./generated_returns.xlsx')
subscriptions_df = pd.read_excel('./generated_subscriptions.xlsx')


# Label Encoding을 위한 함수
def label_encode(df):
    label_encoders = {}
    for column in df.select_dtypes(include=['object']).columns:
        le = LabelEncoder()
        df[column] = le.fit_transform(df[column].astype(str))
        label_encoders[column] = le
    return df, label_encoders


# 정규화를 위한 함수
def normalize(df):
    scaler = StandardScaler()
    numeric_columns = df.select_dtypes(include=['number']).columns
    df[numeric_columns] = scaler.fit_transform(df[numeric_columns])
    return df


# 데이터프레임별로 전처리 및 정규화 적용
def preprocess_and_normalize(df):
    df, label_encoders = label_encode(df)

    # 시계열 데이터 처리 (필요에 따라 조정)
    for column in df.select_dtypes(include=['datetime64', 'object']).columns:
        try:
            df[column] = pd.to_datetime(df[column])
            df[column] = df[column].astype('int64') // 10 ** 9  # 타임스탬프로 변환 (초 단위)
        except ValueError:
            pass  # datetime 변환 불가한 열은 무시

    # 클래스 데이터 (0, 1, 2 등)가 있다면 이를 숫자로 변환
    if 'class' in df.columns:
        df['class'] = df['class'].astype(int)

    df = normalize(df)
    return df


# 각 데이터프레임에 대해 전처리 및 정규화 수행
members_df = preprocess_and_normalize(members_df)
orders_df = preprocess_and_normalize(orders_df)
returns_df = preprocess_and_normalize(returns_df)
subscriptions_df = preprocess_and_normalize(subscriptions_df)
```

## :receipt:구매 동향 분석
<div align=center>
  <img src="https://github.com/user-attachments/assets/60915955-b8ac-4993-9922-4e9bf03111b4"width="800px">
  <div align=center><b>Boxplot</b></div>
</div>

<br></br>

<div align=center>
  <img src="https://github.com/user-attachments/assets/95778f68-2cc9-4917-84d9-c1ae338caa30"width="800px">
  <div align=center><b>Correlation Matrix</b></div>
</div>

<br></br>

<div align=center>
  <img src="https://github.com/heowooyoung/SKN01-2nd-1Team/assets/120430842/e5a2acc0-fa21-4b5c-b000-ed942e4953ac"width="800px">
  <div align=center><b>Kmeans Clustering</b></div>
</div>

## :receipt:고객 이탈 분석
<div align=center>
  <img src="https://github.com/user-attachments/assets/7055d4ed-1686-481f-97cc-14b722da7fee"width="800px">
  <div align=center><b>Boxplot</b></div>
</div>

<br></br>

<div align=center>
  <img src="https://github.com/user-attachments/assets/c8539f9b-ec95-4c7b-9752-8161d51f7264"width="800px">
  <div align=center><b>Correlation Matrix</b></div>
</div>

<br></br>

<div align=center>
  <img src="https://github.com/user-attachments/assets/aaec43de-9f42-449f-9b0e-22ade5b9793b"width="800px">
  <div align=center><b>Visualization of Linear Regression Model</b></div>
</div>

# 5. 기술 스택
<div align=left><h3>🕹️ Frontend</div>
<div align=left>
  <img src="https://img.shields.io/badge/Vue.js-4FC08D?style=for-the-badge&logo=Vue.js&logoColor=white">
  <img src="https://img.shields.io/badge/Vuetify-1867C0?style=for-the-badge&logo=Vuetify&logoColor=white">
  <img src="https://img.shields.io/badge/JavaScript-F7D1E?style=for-the-badge&logo=JavaScript&logoColor=white">
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=TypeScript&logoColor=white">
  <img src="https://img.shields.io/badge/D3.js-F9A3C?style=for-the-badge&logo=D3.js&logoColor=white">
  <img src="https://img.shields.io/badge/Axios-5A29E4?style=for-the-badge&logo=Axios&logoColor=white">
</div>

<div align=left><h3>🕹️ Backend</div>
<div aling=left>
  <img src="https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=Django&logoColor=white">
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=MySQL&logoColor=white">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=Docker&logoColor=white">
</div>

<div align=left><h3>🕹️ AI Core</div>
<div align=left>
  <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=FastAPI&logoColor=white">
  <img src="https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=TensorFlow&logoColor=white">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=Python&logoColor=white">
</div>

# 6. Agile Board (애자일 보드)
<b>Vue-Front-end</b>
<div align=left>
  <img src="https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/476ca612-a9da-48d8-9051-0d88acb2bd5a"width="900px">
  <img src="https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/6336d580-952e-4aa4-911c-5c288d1c4612"width="900px">
</div>

<b>Django-Back-end</b>
<div align=left>
  <img src="https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/de4faa18-2d31-4025-abb9-63aa289f0075"width="900px">
  <img src="https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/37de4bfc-846e-4864-838b-68bed2f1880c"width="900px">
</div>

<b>FastAPI-AI</b>
<div align=left>
  <img src="https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/3e5feeb6-3cd1-40f1-bc0c-5514fdc059c5"width="900px">
  <img src="https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/ab4c68b7-1b78-4907-84a8-20b0efe87b06"width="900px">
</div>

# 7. Commit History (커밋 이력)
Vue-Front-end
https://github.com/heowooyoung/HZ-Vue-Frontend/commits/main/

Django-Back-end
https://github.com/heowooyoung/HZ-Django-Backend/commits/main/

FastAPI-AI
https://github.com/heowooyoung/HZ-FastAPI-AI/commits/main/

# 8. 발생한 이슈 내역  

## 우선 순위를 5 단계로 나눠서 관리  

>
실제 서비스를 운영한다는 마인드로 현실 상황에서 발생하는 크고 작은 이슈들이 존재합니다. 이 서비스들에 있어서 회사의 매출에 중요한 것과 중요하지 않은 요인들이 있을 것입니다. 이와 같은 사항들을 실질적으로 고려하여 이슈 관리를 진행합니다.

<b>1. Agile board에 issue 작성</b>
<div align=left>
    <img src="https://github.com/heowooyoung/SKN01-2nd-1Team/assets/120430842/09a85108-65ab-4b52-81e4-442e0d4bfbcb"width="900px">
</div>

<br></br>

<b>2. 엔지니어링 위키에 issue 작성</b>
<div align=left>
    <img src="https://github.com/heowooyoung/SKN01-2nd-1Team/assets/120430842/4d8c8c03-5af9-4ea9-9d7e-fc9912e4e511"width="900px">
    <img src="https://github.com/heowooyoung/SKN01-2nd-1Team/assets/120430842/e44e9749-44e8-4a40-90c9-fa1e0411da2a"width="900px">
    <img src="https://github.com/heowooyoung/SKN01-2nd-1Team/assets/120430842/55708875-8901-4e12-844d-cb942382378e"width="900px">
</div>

<br></br>

<b>3. Team Project 자체 issue 작성</b>
<div align=left>
    <img src="https://github.com/heowooyoung/SKN01-2nd-1Team/assets/120430842/62e14a59-9c3f-4f45-bab1-cf8fbb0c6815"width="900px">
</div>

# 9. ERD
![image](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/2868a2f3-009e-4afc-8d20-37c0f040e172)

# 10. 주요 Domain 요소들
<div><b><i>Front-end</i></b></div>
Home, Product, Subscription, Food, Drink, Movie, Admin, Order, Cart, Account
<br></br>
<div><b><i>Django-Back-end</i></b></div>
Account, Food, Movie, drink, Product, MovieAPI, Order, Subscribe, Authentication
<br></br>
<div><b><i>FastAPI-AI</i></b></div>
Board, analysis, fake_data, predict, tool



# 11. 한 줄 회고
- 도메인 구조 결정과 데이터 관점에서 많은 고민이 필요했으며, 효과적인 분석 방법에 대한 경험 부족을 느꼈습니다.
- 뷰 문법과 Django API 통신에 대해 많이 배웠지만, 계획과 달리 뷰를 많이 다루게 되어 아쉬웠습니다. 앞으로는 더 체계적으로 진행하고, 마감기한에 맞춰 생산성을 높이는 방법을 고민해야될 것 같습니다.
