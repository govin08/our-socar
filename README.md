# 아이펠톤 쏘카3기 "우리 쏘카 타"
# 구성원
- **차윤겸(팀장)**
- 김선중(팀원)
- 김연수(팀원)
- 배현우(팀원)
- 이승준(팀원)

# 주제
> 카셰어링에서의 데이터기반 수요 예측

## 세부주제

# 노션 주소
https://www.notion.so/modulabs/e9651dcbc43c4d0e95954ef1963426f1

# 깃허브 내 폴더 구조도

our-socar
- 1차윤겸
- 2김선중
- 3김연수
- 4배현우
- 5이승준
- main
    - code
        - code_a_collect_data
        - code_b_clustering
        - code_c_forecasting
            - code_ca_ARIMA
            - code_cb_LSTM
    - data
        - data_a_original
        - data_b_raw
        - data_c_intermediate
        - data_d_final
    - document
- .git
- readme.md

<!--파일구조도 개선 필요 있음
https://jane-aeiou.tistory.com/80-->

# 파일 양식

## main 폴더의 파일 양식
- 예시 : `2b201_1229_population.csv`
- `2b201`
  - 맨 앞 숫자 `2b` (용도)
    - 1 : 프로그램
    - 2 : 데이터
        - a : original 파일 (각자 수집한 원본 csv 파일, 한 개 feature)
        - b : raw 파일 (엑셀로 작업하여 변경한 csv 파일, 한 개 feature)
        - c : intermediate 파일 (주피터 노트북으로 작업하여 변경한 csv 파일, 한 개 feature)
        - d : final 파일 (최종 csv 파일, 여러 개 feature)
    - 3 : 문서
  - 두번째 숫자 `2` (작성자, 가나다순)
    - 1 : 차윤겸
    - 2 : 김선중
    - 3 : 김연수
    - 4 : 배현우
    - 5 : 이승준
  - 세번째, 네번째 숫자 `01` : 임의번호
- `1229` : 작성날짜
- `population.csv` : 파일명 (description)

## 개인 폴더의 파일 양식
- 자율
