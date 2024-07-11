# SKN01-2nd-1Team
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
- HZ
- 정의헌: JUNGUIHEON
- 최인헌: ih9511
- 허우영: heowooyoung
- 이재호: gigcot
- 임영훈: yhoon3002

# 2. 프로젝트 개요
- 프로젝트 명: Waiting
- 프로젝트 소개: 모든 OTT의 독점 서비스를 Waiting에서 전부 사용 가능하다!
- 프로젝트 필요성(배경): OTT 서비스를 한 눈에 볼 수 없어서 여러 서비스 사이트에서 구독을 해야 하는데 이걸 하나로 이용할 수 없을까 ? 에서 시작 되었습니다.
- 프로젝트 목표: 웹 페이지 구현 및 데이터 분석

# 3. 기술 스택
- Python, Django, SQLAlchemy, FastAPI, MYSQL, Docker, Redis, HTML5/CSS3, JavaScript, Vue3, Vuetify3, TensorFlow, Keras, axios, Graphviz, 

# 4. Agile Board (애자일 보드)
Vue-Front-end
![image](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/476ca612-a9da-48d8-9051-0d88acb2bd5a)
![image](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/6336d580-952e-4aa4-911c-5c288d1c4612)

Django-Back-end
![image](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/de4faa18-2d31-4025-abb9-63aa289f0075)
![image](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/37de4bfc-846e-4864-838b-68bed2f1880c)

FastAPI-AI
![image](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/3e5feeb6-3cd1-40f1-bc0c-5514fdc059c5)
![image](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/ab4c68b7-1b78-4907-84a8-20b0efe87b06)

# 5. Commit History (커밋 이력)
Vue-Front-end
https://github.com/heowooyoung/HZ-Vue-Frontend/commits/main/

Django-Back-end
https://github.com/heowooyoung/HZ-Django-Backend/commits/main/

FastAPI-AI
https://github.com/heowooyoung/HZ-FastAPI-AI/commits/main/

# 6. 발생한 이슈 내역  

## 우선 순위를 5 단계로 나눠서 관리  

```c
실제 서비스를 운영한다는 마인드로 현실 상황에서 발생하는 크고 작은 이슈들이 존재할 것입니다.
이 서비스들에서 회사 입장에서 매출에 중요한 것과 중요하지 않은 것들이 있을 것입니다.
이와 같은 사항들을 실질적으로 고려하여 이슈 관리를 진행합니다.
```
1. agile board 의 issue칸에 작성
![image](https://github.com/heowooyoung/SKN01-2nd-1Team/assets/120430842/09a85108-65ab-4b52-81e4-442e0d4bfbcb)

2. 엔지니어링 위키에 issue 작성
![image](https://github.com/heowooyoung/SKN01-2nd-1Team/assets/120430842/4d8c8c03-5af9-4ea9-9d7e-fc9912e4e511)
![image](https://github.com/heowooyoung/SKN01-2nd-1Team/assets/120430842/e44e9749-44e8-4a40-90c9-fa1e0411da2a)
![image](https://github.com/heowooyoung/SKN01-2nd-1Team/assets/120430842/55708875-8901-4e12-844d-cb942382378e)

3. Team Project 자체 issue 작성 
![image](https://github.com/heowooyoung/SKN01-2nd-1Team/assets/120430842/62e14a59-9c3f-4f45-bab1-cf8fbb0c6815)

이상입니다.

# 7. ERD
![image](https://github.com/SKNETWORKS-FAMILY-AICAMP/SKN01-2nd-1Team/assets/120430842/2868a2f3-009e-4afc-8d20-37c0f040e172)

# 8. 주요 Domain 요소들
Vue-Front-end
Home, Product, Subscription, Food, Drink, Movie, Admin, Order, Cart, Account

Django-Back-end
Account, Food, Movie, drink, Product, MovieAPI, Order, Subscribe, Authentication

FastAPI-AI
Board, analysis, fake_data, predict, tool

# 9. 수행결과(테스트/시연 페이지)
https://www.youtube.com/watch?v=Mcd3E41yM1c
![image](https://github.com/heowooyoung/SKN01-2nd-1Team/assets/120430842/e5a2acc0-fa21-4b5c-b000-ed942e4953ac)

# 10. 한 줄 회고
- "도메인 구조 결정과 데이터 관점에서 많은 고민이 필요했으며, 효과적인 분석 방법에 대한 경험 부족을 느꼈다.
- 뷰 문법과 Django API 통신에 대해 많이 배웠지만, 계획과 달리 뷰를 많이 다루게 되어 아쉬웠다. 앞으로는 더 체계적으로 진행하고, 마감기한에 맞춰 생산성을 높이는 방법을 고민해야겠다."
