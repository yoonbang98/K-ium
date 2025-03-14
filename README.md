## 뇌동맥류 예측 AI - K-ium 의료 인공지능 경진대회 (Team VITAL)
### 📌 프로젝트 개요
본 프로젝트는 2023 K-ium 의료 인공지능 경진대회를 위해 Team VITAL이 개발한 AI 모델로, 뇌혈관 조영술 영상을 활용하여 뇌동맥류의 존재 여부 및 위치를 예측하는 알고리즘을 구현했습니다.

### 🎯 프로젝트 목표
**딥러닝 모델을 활용하여 뇌동맥류 유무 및 위치를 예측하는 AI 알고리즘 개발**

### 💡 프로젝트 과정
#### 📊 데이터 전처리 및 증강
* 데이터셋: 1,127명의 환자로부터 총 9,016개의 뇌혈관 조영술 이미지 (각 환자당 LI, LV, RI, RV 2장씩 총 8장)
  라벨: 뇌동맥류 존재 여부 (이진 분류) , 뇌동맥류 위치 정보 (21개 카테고리)
* 전처리 과정: 부위별 이미지 자르기 (혈관이 명확하게 나타나도록 특정 영역을 선택) -> 정답값 설정 (동일 환자의 이미지라도 부위별로 다른 정답값을 가질 수 있도록 설계)
* 데이터 증강 기법: 확률적으로 수평/수직 반전, -45° ~ 45° 범위 내에서 무작위 회전
  
#### 🏗️ 모델 개발
* 기반 모델: cs3darknet (CSPNet + DarkNet53)
참고 논문: Wang, Chien-Yao, et al. "CSPNet: A new backbone that can enhance learning capability of CNN." CVPR (2020)
* 뇌동맥류 여부 예측: 한 환자의 8개 뇌 영상에서 예측된 확률값을 평균하여 최종 예측 수행
* 뇌동맥류 위치 예측 전략: 위치 정보 데이터가 부족하여 모든 부위 예측이 어려움 -> 통계적으로 가장 빈도가 높은 L_ICA, R_LCA에 대한 예측 수행

#### 🚀 최종 성능 및 한계점
|                        | AUROC(뇌동맥류 여부) | Accuracy(뇌동맥류 위치) |
|------------------------|------------------|------------------|
| 임시 Test set (index 1001~1052) | 0.889            | 0.96             |
| Test set              | 0.741            | 0.957            |
* 강점: 사전학습 CNN 모델을 활용한 높은 예측 정확도, 부위별 전처리 및 데이터 증강 기법 적용으로 모델의 성능 향상
* 한계점: 위치 예측을 위한 데이터 부족, 앙상블 모델 적용 필요

#### 🏆 수상 내역
**🥇 2023 K-ium 의료 인공지능 경진대회 1위 수상**
