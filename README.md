# SDP Infra Data Project

> 코로나19로 인해 영향을 받은 인프라 건설 및 투자 관련 기사를 오픈소스에서 수집 및 자동 분류하여 DB에 저장.
유사 인프라 건설 현장끼리 분류하여 비슷한 성질을 가진 인프라 현황 파악.
> 

## 1. 프로젝트 개요

- 개발 기간: 2020.04 - 2020.12.
- 참여 인원: 20명
- 맡은 역할: 프로젝트 매니저(PM) 및 NLP 개발자
- 활용 데이터: 직접 수집한 인프라 건설 현장 관련 기사들 (한 달에 약 10만 건)
- 사용 기술 / 데이터 분석 방법:
    - 오픈소스 자료 수집: Python Scrapy, 각종 Search APIs
    - 기사 자동 분류: Python, NLP(TF-IDF와 Logistic Regression, GloVe와 LSTM)
    - 유사 인프라 건설 현장 탐색: 연관규칙분석(장바구니분석)

## 2. 프로젝트 핵심 내용 및 역할

- 오픈소스 자료 수집 및 분류
    - 프로젝트 설명
        - 본 프로그램은 인프라 건설 및 투자 관련 기사를 자동으로 수집해 주는 프로그램으로,
        ”검색 키워드 선정 - Scrapy 및 Search API로 기사 제목 수집 - 기사 원문 추출 - NLP로 분류 - DB에 저장’이라는 파이프라인에 따라 동작한다.
        - 프로그램 Documentation (전체 코드는 계약 규정에 따라 공개 불가)
            
            [AI_Document_Classifier_for_PPI_Deal_Status_Prediction.pdf](https://drive.google.com/file/d/1XX8NKFBrAo1FJa3c0qAtmuZndjj-iqC_/view?usp=drivesdk)
            
    
    - 맡은 역할과 한 일
        - 프로젝트 매니저(PM)
            - 월드뱅크의 요청 정리 및 문제 규정
            - 리서치팀과 개발팀 사이에서 커뮤니케이션하며 데이터 수집 파이프라인 기획
            - 리서치팀과 데이터를 수작업으로 수집하며 연관성 높은 검색 키워드 선정
            - 개발팀과 Scrapy와 API로 수집 실험을 진행하며 가장 효과적인 데이터 수집 방법 탐색
        - NLP 개발자
            - 사람이 기사를 직접 읽지 않아도 인프라 건설 현장의 상황을 알 수 있을까?
                - [인프라 건설 현장의 status (활성 - Operation / Active, 비활성 - Cancel / Delay)에 따른 단어들에는 무엇이 있을까?](https://github.com/sjeonglee/sdp-vocab-selector)
                    - Word Counting
                    - Word Appearance
                    - 회귀분석으로 vocab의 중요성에 따라
                    - 의사결정나무
                - [리서치팀이 수작업으로 분류해 준 기사들을 바탕으로 TF-IDF 벡터 추출, 기사의 내용에 따라 활성 혹은 비활성으로 분류할 수 있는 Logistic Regression 모델 개발](https://github.com/sjeonglee/SDP-Infra-Data-Project/blob/main/TFIDF_LOGREG_MODEL_EVALUATION.ipynb)
                - XGBoost, MLP(MultiLayer Perception), RNN 모델과 앙상블하여 활용함
            - 인프라 관련 기사가 아닌 기사들이 수집되었을 때, 관련 기사만 추출하는 방법은?
                - [인프라 관련 기사들에서 공통된 단어들을 추출, Pre-Trained GloVe 벡터와 LSTM 모델을 활용하여 인프라 관련 기사인지 판단하는 모델 개발](https://github.com/sjeonglee/SDP-Infra-Data-Project/blob/main/Classification_GloVe.ipynb)
            - 특정 인프라 건설 프로젝트와 유사한 성질을 가진 다른 프로젝트를 찾을 수 있을까?
                - [각 프로젝트 별 특징이 정리된 엑셀 파일을 바탕으로 연관규칙분석(장바구니 분석) 수행](https://github.com/sjeonglee/SDP-Infra-Data-Project/blob/main/map_see_also.ipynb)

## 3. 프로젝트 핵심 성과

- 최종 앙상블 모델의 Accuracy 86.05%, F1-score 0.716
- 월드뱅크 싱가폴과의 협업 추진 및 약 700만원 규모의 프로젝트 계약 유치
- 월드뱅크 단기컨설턴트로 채용됨 (2020.05. - 2021.06.)
- 지속가능 인프라 개발 관련으로 연세대학교 고등교육혁신원 워크스테이션에서 2학기 연속 투자 유치
