# 🏥 난임 환자 임신 성공 여부 예측 AI

> AI 헬스케어 3기 해커톤 · Public Leaderboard **3위** · AUC **0.74235**

## 📌 프로젝트 개요
## 🔗 팀 레포: https://github.com/bhw-rgb/AI-Hackathon-Predicting-Pregnancy-Success-for-Infertile-Patients
난임 환자의 임상 데이터를 분석하여 임신 성공 여부를 예측하는 이진 분류 AI 모델입니다.

| 항목 | 내용 |
|------|------|
| 데이터 | 영국 HFEA |
| Train | 256,351건 · 62개 변수 |
| Test | 90,067건 |
| 타겟 | 임신 성공 여부 (실패 74.17% / 성공 25.83%) |
| 평가지표 | ROC-AUC |

## 🏆 최종 성능

| 지표 | 점수 |
|------|------|
| 본인 CV AUC | 0.7398 |
| 팀 Public LB AUC | 0.74235 (3위) |
| F1 Score | 0.5166 |

※ 최종 제출 모델은 팀원 전체 실험 결과를 블렌딩한 팀 공동 산출물

## 👤 본인 담당 브랜치

`feature/이승혁-EDA` · `feature/이승혁-전처리` · `feature/이승혁-모델학습` · `feature/이승혁-튜닝` · `feature/이승혁-SHAP분석` · `feature/이승혁-피처엔지니어링` · `feature/이승혁-앙상블`

## 🔬 실험 기록 (총 19회)

| 실험 | 모델 | 변경사항 | AUC | 비고 |
|------|------|----------|-----|------|
| Exp-01 | - | EDA · 결측치 처리 | - | 99% 결측 컬럼 5개 삭제 |
| Exp-02 | - | 인코딩 + 이상치 처리 | - | IQR 클리핑 적용 |
| Exp-03 | XGBoost | 베이스라인 | 0.7388 | scale_pos_weight 적용 |
| Exp-04 | XGBoost | 하이퍼파라미터 튜닝 | 0.7391 | RandomizedSearch n_iter=20 |
| Exp-05 | XGBoost | SHAP 분석 | - | 이식된 배아 수 1위 |
| Exp-06 | XGBoost | 피처 엔지니어링 | 0.7394 | 파생 변수 6개 추가 |
| Exp-07 | XGB+LGBM | 앙상블 | 0.7394 | 50:50 가중치 |
| Exp-08 | XGBoost | SMOTE 적용 | 0.7298 | ❌ 성능 저하 → 미적용 |
| Exp-09 | LightGBM | 논문 기반 개선 | 0.7391 | num_leaves=63 추가 |
| Exp-10 | XGBoost | K-Fold 5 vs 10 | 0.7398 | K=5 유지 |
| Exp-11 | XGBoost | Random Search 개선 | 0.7392 | n_iter=60 |
| Exp-12 | XGB+LGBM | 최종 앙상블 | 0.7397 | XGB 60% + LGBM 40% |
| Exp-13 | XGBoost | Optuna 튜닝 | 0.7394 | 개선 없음 |
| Exp-14 | XGBoost | Data Leakage 수정 | 0.7362 | ✅ 전처리 정석화 완료 |
| Exp-15 | XGBoost | 임계값 조정 | 0.7361 | 0.5가 최적 |
| Exp-16 | XGB+LGBM+CatBoost | 3모델 앙상블 | 0.7397 | CatBoost 추가 |
| Exp-17 | XGB+LGBM+CatBoost+LR | 스태킹 앙상블 | 0.7397 | 메타 모델: LR |
| Exp-18 | CatBoost | Optuna 튜닝 50 trial | 0.7398 | depth=7, lr=0.034 |
| Exp-19 | CatBoost | 규칙 완전 준수 최종 | 0.7395 | fold 내 IQR 클리핑 |

## 🔍 SHAP 변수 중요도

| 순위 | 변수 | 영향 |
|------|------|------|
| 1 | 이식된 배아 수 | +0.36 |
| 2 | 시술 당시 나이 | +0.32 |
| 3 | 저장된 배아 수 | +0.29 |
| 4 | 배아 이식 경과일 | -0.22 |

## ⚠️ Data Leakage 방지 원칙
✅ 전처리는 항상 train에서만 fit
✅ valid / test에는 transform만 적용
✅ CV 시 scaler · imputer · encoder도 fold 안에서 재fit
✅ 점수 차이가 작아도 정규 대회에서는 실제 결과가 바뀔 수 있음

## 📚 참고 논문

| 논문 | 저자 | 연도 | 적용 내용 |
|------|------|------|-----------|
| XGBoost: A Scalable Tree Boosting System | Chen & Guestrin | 2016 | 베이스라인 모델 |
| A Unified Approach to Interpreting Model Predictions | Lundberg & Lee | 2017 | SHAP 분석 |
| LightGBM | Ke et al. | 2017 | 앙상블 모델 |
| SMOTE | Chawla et al. | 2002 | 불균형 처리 실험 |
| Cross-Validation and Bootstrap | Kohavi | 1995 | 교차검증 방법론 |
| Random Search for Hyper-Parameter Optimization | Bergstra & Bengio | 2012 | 하이퍼파라미터 튜닝 |
| An interpretable ML model for IVF | Fanton et al. | 2022 | 난임 예측 참고 |

## 🛠 기술 스택

`Python` `XGBoost` `LightGBM` `CatBoost` `Optuna` `SHAP` `Scikit-learn` `Pandas` `NumPy` `Git`
