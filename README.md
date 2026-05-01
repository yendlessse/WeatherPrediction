# 🌦️ Weather Prediction Project

이 프로젝트는 기상 관측 데이터를 바탕으로 **'맑음', '흐림', '비'**의 3가지 날씨 상태를 예측하는 머신러닝 모델을 구축한 프로젝트입니다.

## 🛠️ 작업 프로세스 및 분석 내용

### 1. 데이터 탐색 및 특징 분석 (EDA)
*   **주요 변수**: 기온(C), 풍속(m/s), 습도(%), 증기압(hPa), 이슬점(C), 기압(hPa), 운량(cloud), 풍향(sin/cos) 등
*   **특징 중요도 분석**: `featureImportance.png`를 통해 분석한 결과, **운량(cloud)**이 모델 예측에 가장 압도적인 영향을 주는 핵심 변수임을 확인했습니다.

### 2. 모델 선택 및 최적화 전략
초기 **RandomForest** 모델에서 시작하여 점진적으로 성능을 고도화했습니다.

*   **RandomForest**: 초기 베이스라인 모델로 사용.
*   **XGBoost**: 오차를 보완하며 학습하는 부스팅 알고리즘으로 전환하여 성능을 쥐어짜는 전략 선택.
*   **하이퍼파라미터 튜닝**: `n_estimators`, `learning_rate`, `max_depth` 등을 조정하여 과적합을 방지하고 일반화 성능을 확보했습니다.

### 3. 주요 기법 (Key Techniques)
*   **Feature Engineering**: 기상학적 특성을 반영하기 위해 변수 간의 관계를 분석했습니다.
*   **K-Fold 교차 검증**: 데이터 분할의 우연성을 배제하고 모델의 실제 실력을 검증하기 위해 `cv=5` 설정을 활용했습니다.
*   **Overfitting 방지**: `subsample`, `colsample_bytree` 설정을 통해 특정 변수에 과하게 의존하지 않도록 규제했습니다.

## 📈 모델 성능 (Model Performance)

단계별 성능 향상 수치는 다음과 같습니다.

| 단계 | 적용 모델 | Validation Accuracy | 비고 |
| :--- | :--- | :--- | :--- |
| **Step 1** | RandomForest | **0.7087** | 초기 베이스라인 |
| **Step 2** | Feature Engineering | **0.7354** | 파생변수 만들기 |
| **Step 2** | XGBoost (Base) | **0.7694** | 알고리즘 전환 후 급성장 |
| **Step 3** | **Ensemble** | **0.7839** | 모델 안정성 및 신뢰도 검증 완료 |

---

## 🚀 실행 및 결과 저장
*   최종 모델은 `Submission_example.csv` 양식에 맞춰 `weather label` 컬럼을 포함한 `pred.csv` 파일로 결과를 출력합니다.
