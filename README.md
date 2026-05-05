
# 🌦️ Weather Prediction Model (ML Pipeline Evolution)

## 📌 프로젝트 개요

기상 데이터를 기반으로 날씨 상태(`weather label`)를 예측하는 머신러닝 모델
단순 모델에서 시작하여 점진적으로 성능을 개선하며 **앙상블 기반 고성능 모델**까지 발전

---

## 🚀 모델 발전 과정

### 1️⃣ Baseline (Notebook Version)

> `baseline.ibynb`

#### ✔ 특징

* RandomForest / XGBoost 단일 모델 실험
* Train/Test Split 기반 검증
* 기본적인 Feature Engineering 적용

#### ✔ 한계

* 데이터 분할이 단순하여 **일반화 성능 부족**
* 모델 성능 불안정

---

### 2️⃣ Improve Version (Stacking)

> `WeatherPrediction2.ibynb`

#### ✔ 개선 내용

* `StratifiedKFold` 적용 (데이터 분포 유지)
* XGBoost + RandomForest → **Stacking Ensemble**
* Meta Model: Logistic Regression

#### ✔ 핵심 구조

```
XGB + RF → Logistic Regression → 최종 예측
```

#### ✔ 결과

* OOF 기반 평가로 **신뢰도 상승**
* Baseline 대비 성능 향상
* 하지만 구조가 복잡하고 과적합 가능성 존재

<img width="576" height="455" alt="fold_accuracy_imporve" src="https://github.com/user-attachments/assets/dab40eaa-e2f3-4163-9ae8-511bc4ca3246" />


---

### 3️⃣ Improve Voting Version

> `WeatherPrediction2.ibynb`
> 
#### ✔ 개선 내용

* Stacking → **Soft Voting Ensemble**로 변경
* XGB + RF 확률 평균 방식

#### ✔ 핵심 구조

```
(XGB + RF) → 확률 평균 → 최종 예측
```

#### ✔ 장점

* 구조 단순화
* 학습 속도 개선
* 과적합 위험 감소

#### ✔ 결과

* Stacking 대비 안정적인 성능
* 유지보수 및 디버깅 용이

---

### 4️⃣ Advanced Version (Final Model)

> `WeatherPrediction2.ibynb`

#### ✔ 주요 개선 사항

* 모델 다양성 확대:

  * XGBoost
  * HistGradientBoosting
  * CatBoost
* **Soft Voting Ensemble**
* 결측치 처리 제거 → 모델의 Native Handling 활용
* 고급 Feature Engineering 추가

#### ✔ 핵심 구조

```
XGB + HGB + CatBoost → Soft Voting → 최종 예측
```

#### ✔ 추가된 Feature

* `humidity_temp_ratio`
* `pressure_temp_ratio`

#### ✔ 결과 (Cross Validation)

<img width="576" height="455" alt="fold_accuracy_advanced" src="https://github.com/user-attachments/assets/5aa9e0a1-20a4-4f86-b27e-9c12011214d3" />


평균 OOF Accuracy ≈ 0.78 ~ 0.79
---

## 📊 모델 비교 요약

| 모델       | 방식                 | 특징      | 안정성 | 성능 |
| -------- | ------------------ | ------- | --- | -- |
| Baseline | 단일 모델              | 단순 구조   | ❌   | 낮음 |
| Improve  | Stacking           | 복잡한 앙상블 | ⚠️  | 중간 |
| Voting   | Soft Voting        | 단순 + 안정 | ⭕   | 중상 |
| Advanced | Multi Model Voting | 고급 앙상블  | ⭕   | 최고 |

---

## 💡 최종 결론
<img width="567" height="455" alt="Model Performance Comparison" src="https://github.com/user-attachments/assets/c6a004dc-fa59-4844-ad1b-e9dcaf5576bb" />


* 단순한 모델보다 **앙상블 모델이 성능 향상에 효과적**
* Stacking보다 **Soft Voting이 더 안정적인 결과 제공**
* 모델 성능 향상의 핵심은:

  1. 다양한 모델 조합
  2. 적절한 Feature Engineering
  3. K-Fold 기반 검증

👉 최종적으로
**“Advanced Soft Voting Ensemble 모델이 가장 좋은 성능과 안정성을 보였다.”**

---

## ⚠️ 추가 인사이트

* 과도한 Feature Engineering은 오히려 과적합을 유발할 수 있음
* 모델이 복잡해질수록 반드시 **검증 전략(K-Fold)**이 필요
* CatBoost는 성능 향상에 기여하지만 필수 요소는 아님

---

## 🛠️ 사용 기술

* Python
* Pandas / NumPy
* Scikit-learn
* XGBoost
* CatBoost

---

## ✨ 한 줄 정리

> 단순 모델 → Stacking → Voting → Advanced Ensemble로 발전하며
> **성능과 안정성을 동시에 확보한 머신러닝 파이프라인을 구축했다.**

