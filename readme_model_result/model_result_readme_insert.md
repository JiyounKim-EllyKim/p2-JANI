# 🔍 AI Model Training Results

본 문서는 음악 스트리밍 서비스 사용자 데이터를 기반으로 구독 이탈 예측 모델을 학습하고 성능을 비교한 결과를 정리한 것이다.  
여러 머신러닝 모델을 이용하여 baseline 성능을 비교하고, 이후 Boosting 기반 모델을 중심으로 하이퍼파라미터 튜닝을 수행하였다.  
각 모델의 Accuracy, F1-score, ROC-AUC를 기반으로 성능을 분석하고 최종 모델을 선정하였다.

---

# 📊 Baseline Model Comparison

먼저 다양한 머신러닝 모델을 사용하여 **baseline 성능 비교**를 진행하였다.

### Test Performance

| Model | Accuracy | F1 | ROC-AUC |
|------|------|------|------|
| LogisticRegression | 0.680 | 0.691 | 0.752 |
| SVC | 0.789 | 0.796 | 0.875 |
| CatBoost | <strong><span style="color:#e74c3c">0.849</span></strong> | <strong><span style="color:#e74c3c">0.851</span></strong> | <strong><span style="color:#e74c3c">0.942</span></strong> |
| XGBoost | <strong><span style="color:#e74c3c">0.849</span></strong> | <strong><span style="color:#e74c3c">0.852</span></strong> | <strong><span style="color:#e74c3c">0.942</span></strong> |
| LightGBM | <strong><span style="color:#e74c3c">0.849</span></strong> | <strong><span style="color:#e74c3c">0.852</span></strong> | <strong><span style="color:#e74c3c">0.942</span></strong> |
| RandomForest | 0.814 | 0.818 | 0.900 |

Baseline 비교 결과 **Gradient Boosting 계열 모델(CatBoost, XGBoost, LightGBM)** 이 가장 높은 성능을 보였다.  
따라서 해당 모델들을 중심으로 **하이퍼파라미터 튜닝을 진행하였다.**

---

# ⚙️ Hyperparameter Tuning

Boosting 모델에 대해 **HyperOpt 기반 Bayesian Optimization (TPE)** 을 이용하여  
하이퍼파라미터 탐색을 진행하였다.

### Final Performance

| Model | Accuracy | F1 |
|------|------|------|
| XGBoost | <strong><span style="color:red">**0.8485**</span></strong> | <strong><span style="color:red">**0.8484**</span></strong>| 
| LightGBM | 0.8476 | 0.8473 |
| CatBoost | 0.8471 | 0.8470 |

세 모델 모두 약 **0.85 수준의 Accuracy와 F1-score**를 기록하며 매우 유사한 성능을 보였다.

---

# 📈 ROC Curve Comparison

<p align="center">
<img src="readme_model_result/images/models_roc.png" width="550">
</p>

세 모델 모두 **ROC-AUC 약 0.94 수준의 높은 분류 성능**을 보였다.

| Model | ROC-AUC |
|------|------|
| XGBoost | <strong><span style="color:red">0.9421</span></strong>|
| LightGBM | 0.9415 |
| CatBoost | 0.9385 |

---

# 🏆 Final Model Selection

튜닝 결과 세 Boosting 모델은 모두 유사한 성능을 보였으며,  
그 중 **XGBoost 모델이 가장 높은 성능을 기록하였다.**

따라서 본 프로젝트의 **최종 모델은 XGBoost로 선정하였다.**