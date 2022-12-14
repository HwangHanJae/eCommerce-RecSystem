  # 이커머스 상품 추천 시스템

## 프로젝트 개요
- **이커머스 고객 행동데이터를 기반으로 상품 추천 시스템**을 구축하였습니다.
- **전환이 일어난 고객**, **전환이 일어나지 않은 고객으로 집단을 나누어** 상품을 추천하였습니다.
  - 전환 : 고객이 제품을 장바구니에 담거나 구매를 한 경우
- 사용한 모델로는 [implicit 라이브러리](https://github.com/benfred/implicit)를 사용했습니다.
## 프로젝트 배경 및 목적

가상의 이커머스의 데이터분석가라 가정하여 **자사의 
이커머스 비즈니스의 매출증대를 목표**로 프로젝트를 진행하였습니다.

## 데이터 정보
<img width=700 alt="image1" src="https://user-images.githubusercontent.com/60374463/196103676-121d7fb8-5d03-4757-ad62-a2ae90ed0cf0.png">
<!--![image](https://user-images.githubusercontent.com/60374463/196103676-121d7fb8-5d03-4757-ad62-a2ae90ed0cf0.png)-->

출처 : https://www.kaggle.com/datasets/mkechinov/ecommerce-behavior-data-from-multi-category-store

데이터 크기 : 약 5gb

행 : 약 4200만개

열 : 9개

## 프로젝트 과정
1. **데이터 경량화(5gb -> 1gb)**
- 데이터 타입 변경
  - object -> category
  - float64, int64 -> float32, int32
  - csv -> parquet
2. **데이터 전처리**
- GMT+4 국가의 이커머머스로 가정 event_time 컬럼 전처리
  - UTC 문자 제거
  - event_time 컬럼에 4시간 더하기
  - 11월 이후 데이터 제거
3. **데이터 분석 및 인사이트 도출**
4. **implicit 라이브러리**를 이용하여 **추천시스템 구축**
5. **추천시스템 성능 평가 및 개선**
## 데이터 분석 및 결과

해당 결과는 아래의 링크를 통하여 확인할 수 있습니다.
- [pandas_eda.ipynb](https://github.com/HwangHanJae/eCommerce-RecSystem/blob/main/EDA/pandas_eda.ipynb)
- [pandas_eda_ver2.ipynb](https://github.com/HwangHanJae/eCommerce-RecSystem/blob/main/EDA/pandas_eda_ver2.ipynb)

이커머스의 **매출증대에는 고객의 전환율, 방문자 수의 증가가 중요한 요인**입니다.

이커머스의 매출증대를 위하여 **전환이 일어나지 않은 고객, 전환이 일어난 고객으로 분류**하여 **사이트 이용률**을 확인해보았습니다.

<img width=700 alt="image1" src="https://user-images.githubusercontent.com/60374463/195752119-b4eab29e-1b65-4dec-b9c4-a7e86c595d75.png">
<!--![image](https://user-images.githubusercontent.com/60374463/195752119-b4eab29e-1b65-4dec-b9c4-a7e86c595d75.png)-->

<img width=700 alt="image1" src="https://user-images.githubusercontent.com/60374463/195752172-da5afeb5-14bf-40dd-b451-66c93512e094.png">
<!--![image](https://user-images.githubusercontent.com/60374463/195752172-da5afeb5-14bf-40dd-b451-66c93512e094.png)-->

**전환이 일어난 고객의 사이트 이용률이 그렇지 않은 고객들 보다 더 높다는 것을 확인**하였습니다.

고객들이 구매를 하지 않는 이유를 [웹 로그 분석을 통한 소비자 구매지연행동 연구 논문](https://s-space.snu.ac.kr/handle/10371/134013)에서 찾을 수 있었습니다.

| **이커머스 시장의 성장에 따라 상품이 많아지는 장점이 존재**했지만  
| **상품이 많아짐에 따라 소비자가 선택해야하는 대안이 많아지고 소비자는 대안을 선택하는 과정에서 부정적인 감정**을 겪게 됩니다.  
| 이때 **부정적인 감정을 회피하기 위하여 구매지연행동**이 나오게 됩니다.

소비자에게 좀 더 적합한 대안을 추천해 대안을 선택할 때 더 좋은 선택을 할 수 있도록 추천시스템을 구축하였습니다.


## 추천 시스템
해당 결과는 [Recomendation/Recomendation_Model.ipynb](https://github.com/HwangHanJae/eCommerce-RecSystem/blob/main/Recommendation_Test/Recomdation_Model.ipynb)를 통하여 확인할 수 있습니다.

### 과정
1. 데이터 전처리 진행 후 **11월 넘어가는 데이터를 제거**
2. **전환이 일어나지 않은 고객, 전환이 일어난 고객을 두 집단**으로 나누기
3. 각 집단에 대하여 **User-Item Matrix(Sparse Matrix)를 생성**
4. **[implicit 라이브러리](https://github.com/benfred/implicit)** 사용하여 **추천시스템 구축**
5. 튜닝 함수 작성 및 **성능 개선**

### 최종성능
<img width=700 alt="image1" src="https://user-images.githubusercontent.com/60374463/195752222-5786207d-6873-41d6-9083-b96c2fd5b723.png">
<!--![image](https://user-images.githubusercontent.com/60374463/195752222-5786207d-6873-41d6-9083-b96c2fd5b723.png)-->

### 추천 결과

<img width=700 alt="image1" src="https://user-images.githubusercontent.com/60374463/195752232-859c520d-4a42-4c49-be78-11c2b77c9686.png">
<!--![image](https://user-images.githubusercontent.com/60374463/195752232-859c520d-4a42-4c49-be78-11c2b77c9686.png)-->
<img width=700 alt="image1" src="https://user-images.githubusercontent.com/60374463/195752241-765e5ebc-2755-4f46-9c0d-d24625b48485.png">
<!--![image](https://user-images.githubusercontent.com/60374463/195752241-765e5ebc-2755-4f46-9c0d-d24625b48485.png)-->


## 회고

### 잘한점/만족한 점
- 추천 모델의 성능개선(기준모델 -> 가중치 조절 -> 튜닝)을 시도하고 성공한 점
- 추천의 결과를 쉽게 알아볼 수 있도록 함수 작성 및 모듈화를 시킨 점

### 아쉬운 점
- 이커머스 도메인의 부족으로 다양한 분석결과와 인사이트를 도출하지 못한 점
- 사용자가 제품에 대한 평가를 내린 선호도와 같은 explicit feedback 데이터가 없다는 점
- lightfm, surprise와 같은 다양한 추천 라이브러리를 사용해보지 못한 점

