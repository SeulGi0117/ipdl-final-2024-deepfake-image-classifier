# 2024 한림대학교 영상처리와딥러닝 기말 프로젝트  
**주제: 딥페이크 이미지 분류**

## Overview
본 프로젝트는 실제 사람 얼굴 이미지와 딥페이크로 합성된 얼굴 이미지를 분류하는 딥러닝 기반 알고리즘을 개발하는 것을 목표로 합니다.  
2024학년도 한림대학교 *영상처리와딥러닝* 수업의 기말 Kaggle 대회 과제로 수행되었습니다.

## Description
- 학습 및 테스트 데이터셋에는 모델 학습과 추론을 방해하는 기술이 적용되어 있습니다.  
- Public leaderboard는 테스트 데이터셋의 10%로 계산되며, 최종 순위는 private accuracy(90%)를 기준으로 결정됩니다.  
- 평가 지표는 **Accuracy** 입니다.  

공식 정의:  
\[
Accuracy = \frac{TP + TN}{TP + TN + FP + FN}
\]

---

## Dataset
- **학습 데이터셋**: 총 5,000장  
  - 실제 이미지(Real): 2,500장  
  - 딥페이크 이미지(Fake): 2,500장  
- **테스트 데이터셋**: 5,000장  
- **제공 파일**
  - `train.csv`: 학습용 데이터 경로 및 레이블
  - `test.csv`: 테스트용 데이터 경로
  - `sample_submission.csv`: 제출 양식 예시  

제출 형식 예시:
ID TARGET
a.jpg 0
b.jpg 0
c.jpg 1
...

---

## Approach

### 1. 데이터 전처리 및 증강
- 데이터셋 크기가 작아 다양한 증강 기법을 적용:  
  - `HorizontalFlip`, `Rotate`, `RandomRain`, `RandomShadow`,  
  - `GaussNoise`, `ISONoise`, `MotionBlur` 등   
- 초기 학습에서는 과도한 증강으로 성능 저하가 있었으며, 이후 적절한 수준으로 조정하여 성능 개선.  

### 2. 모델 선택 및 실험
- **Baseline**: ResNet18 (Adam optimizer, 8 epoch, lr=5e-5)  
- **추가 모델**:
  - EfficientNet_B0  
  - Vision Transformer (ViT)  
  - VGG16  
  - EfficientNet_v2_s   
- 학습 기법:
  - Early stopping, weight decay, learning rate scheduler 적용  
  - 일부 실험에서는 FGSM(Fast Gradient Sign Method) 기반 adversarial training 적용  

### 3. 모델 성능
- EfficientNet 기반 모델이 가장 높은 성능을 기록  
- 앙상블 전략(EfficientNet 2종 + ViT + VGG16)을 통해 최고 **0.97400** accuracy 달성   

---

## Results & Conclusion
- 데이터 증강과 정규화(weight decay, scheduler, early stopping) 기법이 모델 성능에 큰 영향을 주었음  
- EfficientNet이 가장 안정적으로 높은 정확도를 보임  
- 여러 모델을 결합한 앙상블 기법을 통해 단일 모델 성능을 초과하는 결과를 얻음  
### 최종 리더보드 성적
- **Public Accuracy**: 0.97400  
- **Private Accuracy**: 0.96555  
---

## 문서 자료

- [기말 프로젝트 보고서 PDF](./docs/기말프로젝트_보고서_20217137_강슬기.pdf)
- [기말 프로젝트 코드 (Jupyter Notebook)](./docs/기말프로젝트_코드_20217137_강슬기.ipynb)

- 제출 및 데이터셋 관련 파일은 Kaggle 대회 페이지 참고:  
  [Kaggle Competition - IPDL 2024](https://www.kaggle.com/competitions/ipdl-2024/overview)
---
