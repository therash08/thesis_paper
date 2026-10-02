# Experiment 1 — Final Analysis Report

## Experiment Objective

The revised Experiment 1 evaluated whether loneliness-associated and depression-associated Reddit discourse could be distinguished using lexical machine-learning features under a leakage-controlled, author-independent evaluation framework.

The subreddit-derived labels represent discourse-associated categories rather than verified clinical diagnoses.

---

## Methods

Experiment 1: Leakage-Controlled Classification of Loneliness- and Depression-Associated Reddit Discourse

The revised Experiment 1 was designed to determine whether Reddit discourse associated with loneliness and depression could be distinguished using lexical text features under a leakage-controlled and user-independent evaluation framework. Labels represented subreddit-associated discourse categories rather than clinical diagnoses.

Following data integrity auditing and cleaning, exact duplicate content, cross-class duplicate-content conflicts, invalid authors, unusable text, and conflicting post identities were removed. The final cleaned corpus was divided into training, validation, and test partitions using author-grouped stratification. All posts from the same author were restricted to a single partition, preventing user-level information leakage across the training, validation, and test sets.

Text representation was based on TF-IDF features using unigrams and bigrams. The TF-IDF vocabulary was fitted exclusively on the training partition and was subsequently applied unchanged to the validation and test sets. The full representation contained 20,000 features.

Class imbalance was handled primarily through full-data model training rather than random undersampling. Logistic Regression and Linear Support Vector Machine models were evaluated using the full TF-IDF representation. A train-only random undersampling benchmark was retained for methodological comparison, but the full-data strategy was adopted because undersampling discarded a substantial proportion of available training observations without improving validation performance.

Hyperparameters were selected using the training set and the author-disjoint validation set. The untouched test set was not used for hyperparameter selection, threshold selection, feature selection, or model choice. The primary model was frozen before test evaluation as a Linear SVM with C = 0.1, hinge loss, no class weighting, and a frozen decision-function threshold of 0.497099. Logistic Regression was retained as a secondary interpretable model with C = 0.315, balanced class weighting, and a frozen probability threshold of 0.34.

Model performance was assessed using accuracy, balanced accuracy, Macro-F1, Matthews correlation coefficient (MCC), ROC-AUC, class-specific F1 scores, and precision-recall AUC for the loneliness class. Uncertainty on the final test set was quantified using author-cluster bootstrap resampling, in which authors rather than individual posts were sampled with replacement. This preserved within-author dependence during uncertainty estimation.

Additional robustness analyses evaluated the influence of explicit condition-name vocabulary, performance on naturally direct-term-free posts, broader conceptual-cue masking, feature-coefficient stability across models, and coefficient stability under repeated author-level subsampling.

---

## Dataset Split

| split | posts | unique_authors | loneliness_posts | loneliness_percent | depression_posts | depression_percent | depression_loneliness_ratio |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Train | 529852 | 275325.0000 | 105146 | 19.8444 | 424706 | 80.1556 | 4.0392 |
| Validation | 113537 | 58857.0000 | 22530 | 19.8438 | 91007 | 80.1562 | 4.0394 |
| Test | 113535 | 58688.0000 | 22530 | 19.8441 | 91005 | 80.1559 | 4.0393 |
| Total | 756924 |  | 150206 | 19.8443 | 606718 | 80.1557 | 4.0392 |

The final cleaned dataset contained 756,924 posts. Author-grouped splitting prevented the same Reddit author from appearing across training, validation, and test partitions.

---

## Final Independent Test Performance

Values below are reported as point estimate with author-cluster bootstrap 95% confidence intervals.

| Role | Model | Accuracy | Balanced Accuracy | Macro-F1 | MCC | ROC-AUC | PR-AUC (Loneliness) | Loneliness F1 | Depression F1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Primary | Linear SVM | 0.874 (0.870–0.877) | 0.808 (0.800–0.812) | 0.804 (0.799–0.808) | 0.609 (0.599–0.617) | 0.907 (0.901–0.911) | 0.732 (0.724–0.742) | 0.687 (0.679–0.694) | 0.921 (0.918–0.923) |
| Secondary | Logistic Regression | 0.874 (0.871–0.877) | 0.808 (0.800–0.813) | 0.805 (0.800–0.809) | 0.610 (0.600–0.618) | 0.911 (0.905–0.915) | 0.732 (0.723–0.741) | 0.688 (0.680–0.695) | 0.921 (0.919–0.923) |

The Linear SVM remained the pre-specified primary model because model selection was frozen before the independent test set was opened. Logistic Regression was retained as the secondary interpretable model.

---

## Final Test Confusion Matrix

| Model | Correct Loneliness | Loneliness → Depression | Loneliness Correct % | Correct Depression | Depression → Loneliness | Depression Correct % |
| --- | --- | --- | --- | --- | --- | --- |
| Linear SVM | 15725 | 6805 | 69.7958 | 83503 | 7502 | 91.7565 |
| Logistic Regression | 15740 | 6790 | 69.8624 | 83544 | 7461 | 91.8015 |

---

## Validation-to-Test Generalization

| model | metric | validation | test | test_minus_validation | absolute_gap |
| --- | --- | --- | --- | --- | --- |
| Linear SVM | accuracy | 0.8791 | 0.8740 | -0.0051 | 0.0051 |
| Linear SVM | balanced_accuracy | 0.8162 | 0.8078 | -0.0085 | 0.0085 |
| Linear SVM | macro_f1 | 0.8123 | 0.8042 | -0.0081 | 0.0081 |
| Linear SVM | mcc | 0.6248 | 0.6086 | -0.0162 | 0.0162 |
| Linear SVM | roc_auc | 0.9117 | 0.9069 | -0.0048 | 0.0048 |
| Linear SVM | pr_auc_loneliness | 0.7438 | 0.7324 | -0.0114 | 0.0114 |
| Linear SVM | loneliness_f1 | 0.7004 | 0.6873 | -0.0130 | 0.0130 |
| Linear SVM | depression_f1 | 0.9243 | 0.9211 | -0.0032 | 0.0032 |
| Logistic Regression | accuracy | 0.8785 | 0.8745 | -0.0040 | 0.0040 |
| Logistic Regression | balanced_accuracy | 0.8162 | 0.8083 | -0.0079 | 0.0079 |
| Logistic Regression | macro_f1 | 0.8117 | 0.8049 | -0.0068 | 0.0068 |
| Logistic Regression | mcc | 0.6236 | 0.6099 | -0.0137 | 0.0137 |
| Logistic Regression | roc_auc | 0.9150 | 0.9108 | -0.0042 | 0.0042 |
| Logistic Regression | pr_auc_loneliness | 0.7419 | 0.7319 | -0.0099 | 0.0099 |
| Logistic Regression | loneliness_f1 | 0.6996 | 0.6884 | -0.0112 | 0.0112 |
| Logistic Regression | depression_f1 | 0.9238 | 0.9214 | -0.0024 | 0.0024 |

---

## Shortcut-Term Robustness

| Model | Condition | Macro-F1 | MCC | ROC-AUC | PR-AUC Loneliness | Loneliness F1 | Depression F1 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Linear SVM | Original validation | 0.8123 | 0.6248 | 0.9117 | 0.7438 | 0.7004 | 0.9243 |
| Linear SVM | Direct label terms masked | 0.7787 | 0.5577 | 0.8810 | 0.6867 | 0.6432 | 0.9142 |
| Linear SVM | Naturally direct-term-free | 0.7716 | 0.5440 | 0.8708 | 0.6755 | 0.6321 | 0.9111 |
| Linear SVM | Extended cues masked | 0.7693 | 0.5410 | 0.8747 | 0.6789 | 0.6242 | 0.9144 |
| Logistic Regression | Original validation | 0.8117 | 0.6236 | 0.9150 | 0.7419 | 0.6996 | 0.9238 |
| Logistic Regression | Direct label terms masked | 0.7779 | 0.5560 | 0.8878 | 0.6859 | 0.6427 | 0.9132 |
| Logistic Regression | Naturally direct-term-free | 0.7718 | 0.5437 | 0.8772 | 0.6732 | 0.6348 | 0.9088 |
| Logistic Regression | Extended cues masked | 0.7679 | 0.5380 | 0.8821 | 0.6803 | 0.6224 | 0.9135 |

Explicit depression- and loneliness-related vocabulary contributed materially to model performance, but substantial discriminative ability remained among naturally direct-term-free posts.

---

## Cross-Model Top-K Feature Stability

| top_k | absolute_feature_jaccard | depression_feature_jaccard | loneliness_feature_jaccard | union_sign_agreement |
| --- | --- | --- | --- | --- |
| 50.0000 | 0.5625 | 0.4286 | 0.6667 | 1.0000 |
| 100.0000 | 0.5038 | 0.4493 | 0.6000 | 1.0000 |
| 500.0000 | 0.4903 | 0.4859 | 0.6051 | 0.9985 |
| 1000.0000 | 0.5291 | 0.4793 | 0.5835 | 0.9977 |

---

## Author-Level Feature Stability

| model | coefficient_spearman_mean | coefficient_spearman_std | coefficient_pearson_mean | coefficient_pearson_std | top100_jaccard_mean | top100_jaccard_std | top500_jaccard_mean | top500_jaccard_std | top1000_jaccard_mean | top1000_jaccard_std | reference_top500_sign_agreement_mean | reference_top500_sign_agreement_std |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Linear SVM | 0.9276 | 0.0014 | 0.9719 | 0.0004 | 0.8695 | 0.0276 | 0.7852 | 0.0130 | 0.7619 | 0.0136 | 1.0000 | 0.0000 |
| Logistic Regression | 0.9393 | 0.0016 | 0.9708 | 0.0006 | 0.8252 | 0.0282 | 0.7948 | 0.0161 | 0.7529 | 0.0045 | 1.0000 | 0.0000 |

---

## Top Non-Direct Linguistic Features

| Depression-associated feature | Depression coefficient | Loneliness-associated feature | Loneliness coefficient |
| --- | --- | --- | --- |
| suicide | 2.1077 | alone | -4.2320 |
| therapist | 1.9145 | friends | -3.4462 |
| job | 1.8891 | chat | -2.8706 |
| my friends | 1.8523 | dm | -2.7933 |
| suicidal | 1.8220 | lonelier | -2.5687 |
| die | 1.7098 | loneliest | -2.5211 |
| therapy | 1.6739 | conversation | -2.5018 |
| help | 1.5967 | couples | -2.4734 |
| kill | 1.5956 | friend | -2.3699 |
| struggling | 1.5491 | discord | -2.3363 |
| killed | 1.5136 | hmu | -2.3040 |
| fucking | 1.2955 | message | -2.2800 |
| kill myself | 1.2710 | girl | -2.2637 |
| support | 1.2673 | connection | -2.2575 |
| not alone | 1.2603 | friendship | -2.2272 |

---

## Results

Final Independent Test Performance

The frozen models were evaluated once on the untouched author-disjoint test set containing 113,535 posts, including 22,530 loneliness-associated posts and 91,005 depression-associated posts from 58,688 unique authors.

The pre-specified primary Linear SVM achieved an accuracy of 0.874, balanced accuracy of 0.808, Macro-F1 of 0.804, MCC of 0.609, and ROC-AUC of 0.907. Its loneliness-class F1 was 0.687, whereas the depression-class F1 was 0.921. Author-cluster bootstrap analysis estimated a 95% confidence interval of 0.799–0.808 for Macro-F1, 0.599–0.617 for MCC, and 0.901–0.911 for ROC-AUC.

The frozen Logistic Regression model produced very similar classification performance, with accuracy of 0.874, balanced accuracy of 0.808, Macro-F1 of 0.805, MCC of 0.610, and ROC-AUC of 0.911. Its 95% author-cluster bootstrap confidence interval was 0.800–0.809 for Macro-F1 and 0.905–0.915 for ROC-AUC.

The paired author-cluster bootstrap difference in Macro-F1 between the Linear SVM and Logistic Regression was -0.0007, with a 95% interval from -0.0022 to 0.0008. Because this interval included zero, the small numerical difference in Macro-F1 did not provide clear evidence of a meaningful difference between the two models. In contrast, the paired SVM-minus-Logistic-Regression ROC-AUC difference was -0.0039, with a 95% interval from -0.0046 to -0.0032; this interval remained below zero, indicating consistently higher ranking performance for Logistic Regression under the paired bootstrap analysis. The pre-specified Linear SVM nevertheless remained the primary model because model selection had been frozen before the test set was opened.

Robustness to Explicit Condition-Related Vocabulary

Ablation analysis on the validation set showed that explicit depression- and loneliness-related label terms contributed materially to classification. For the Linear SVM, masking direct condition-name terms reduced Macro-F1 from 0.812 to 0.779, a change of -0.034. However, the model retained a Macro-F1 of 0.772 on naturally occurring posts that contained none of the direct condition-name terms. These findings indicate that explicit condition-related vocabulary contributed substantially to discrimination but did not fully account for the model's performance.

Feature Stability and Interpretability

Coefficient patterns were strongly related across the two linear models. The global SVM–Logistic Regression coefficient Spearman correlation was 0.842, the Pearson correlation was 0.902, and coefficient signs agreed for 82.5% of the full 20,000-feature vocabulary.

Feature estimates were also stable under repeated author-level subsampling. The Linear SVM achieved a mean coefficient Spearman correlation of 0.928 with the full-training model, while Logistic Regression achieved 0.939. Mean Top-500 feature-set Jaccard similarity was 0.785 for the Linear SVM and 0.795 for Logistic Regression.

Generalization

Performance decreased only modestly from the author-disjoint validation set to the independent test set. Linear SVM Macro-F1 declined from 0.812 to 0.804, while Logistic Regression Macro-F1 declined from 0.812 to 0.805. The limited validation-to-test change, together with author-disjoint splitting and author-cluster uncertainty estimation, supports the conclusion that the observed discrimination was not solely attributable to overlap between users or duplicated content.

Overall, the results demonstrate that loneliness-associated and depression-associated Reddit discourse can be distinguished with substantial but incomplete accuracy using lexical TF-IDF features. The findings should be interpreted as classification of subreddit-associated discourse rather than diagnosis or identification of clinical mental-health conditions.

---

## Discussion

Key Discussion Points for Experiment 1

1. User-independent generalization

The revised experiment used author-disjoint training, validation, and test partitions. All posts belonging to the same Reddit author were restricted to a single partition. Consequently, the final independent test results were not influenced by the same users appearing during both model development and final evaluation.

2. Effect of class imbalance

The cleaned dataset remained naturally imbalanced, with approximately 80% depression-associated posts and 20% loneliness-associated posts. The primary modelling strategy retained the full training dataset rather than balancing the complete corpus through random undersampling. A train-only undersampling benchmark was evaluated separately. Undersampling substantially reduced the amount of training information available without producing an improvement over full-data modelling.

3. Performance of the two strongest models

The frozen Linear SVM and Logistic Regression models achieved very similar performance on the independent test set. The Linear SVM achieved a Macro-F1 of 0.804 and MCC of 0.609, while Logistic Regression achieved a Macro-F1 of 0.805 and MCC of 0.610.

Paired author-cluster bootstrap confidence intervals for the differences in Macro-F1 and MCC included zero. Therefore, the small numerical differences in these overall classification measures should not be interpreted as evidence that either classifier was clearly superior.

Logistic Regression, however, produced a higher ROC-AUC than Linear SVM on the test set. The paired confidence interval for the SVM-minus-Logistic-Regression ROC-AUC difference remained below zero, indicating consistently stronger ranking performance for Logistic Regression under the bootstrap analysis.

The Linear SVM nevertheless remained the designated primary model because the model-selection rule and primary model had been frozen before the test set was opened.

4. Importance of explicit condition-related terminology

Explicit depression- and loneliness-related terms were among the highest-weighted lexical features. Terms such as "lonely", "depression", "loneliness", and "depressed" occupied the highest coefficient ranks in the linear models.

Masking these direct condition-name terms reduced validation Macro-F1 by approximately 0.034 for both models. This indicates that explicit self-labelling and condition-related vocabulary contributed materially to discrimination.

However, performance did not collapse after removal of these cues. Among naturally occurring validation posts containing none of the direct condition-name terms, both models retained a Macro-F1 of approximately 0.772. Therefore, the models were not relying exclusively on explicit subreddit-associated terminology.

5. Difficulty of loneliness-associated discourse

Loneliness-associated posts were substantially more difficult to classify than depression-associated posts. On the final test set, the Linear SVM achieved a loneliness F1 of approximately 0.687 compared with a depression F1 of approximately 0.921.

Validation error analysis showed that loneliness posts without explicit condition-name terms were particularly difficult. Their error rate was approximately 39%, compared with approximately 13% among loneliness posts containing direct condition-related terminology.

Short loneliness posts were also more difficult to classify than longer posts. This suggests that when explicit self-labelling cues and richer contextual information are absent, loneliness-associated discourse overlaps substantially with language occurring in depression-associated communities.

6. Broader linguistic patterns

After excluding direct depression/loneliness terms, depression-associated features included lexical patterns related to suicide, therapy, help-seeking, work, struggle, and severe distress.

Loneliness-associated features included terms related to friendship, conversation, messaging, social connection, online communication, and interpersonal interaction.

These patterns suggest that the models captured broader differences in discourse in addition to direct condition-name vocabulary. They should nevertheless be interpreted as statistical associations within the Reddit corpus rather than psychological or causal mechanisms.

7. Feature stability

Feature estimates were highly stable across models and across repeated author-level subsampling.

The global coefficient Spearman correlation between Linear SVM and Logistic Regression was approximately 0.842 and the Pearson correlation was approximately 0.902.

Under repeated 80% author-level subsampling, mean coefficient Spearman correlations with the full-training models were approximately 0.928 for Linear SVM and 0.939 for Logistic Regression.

Mean Top-500 feature-set Jaccard similarity was approximately 0.785 for Linear SVM and 0.795 for Logistic Regression, while the directions of the reference Top-500 coefficients were preserved in all subsampling runs.

These findings indicate that the major lexical associations were not highly dependent on a particular subset of Reddit users.

8. Generalization from validation to test

Performance decreased only modestly between the author-disjoint validation and independent test partitions.

Linear SVM Macro-F1 decreased from approximately 0.812 to 0.804, while Logistic Regression decreased from approximately 0.812 to 0.805.

ROC-AUC and class-specific F1 scores also showed relatively small validation-to-test changes. This provides evidence that the fitted models generalized beyond the specific users observed during model development.

9. Interpretation of the labels

The labels in this experiment were derived from subreddit-associated discourse categories. They should not be interpreted as verified clinical diagnoses.

Accordingly, the models distinguish linguistic patterns associated with Reddit communities focused on depression and loneliness. They do not diagnose depression, determine loneliness status, estimate symptom severity, or infer the mental-health condition of an individual Reddit user.

10. Comparison with the earlier Experiment 1

The revised experiment should not be presented as a strict head-to-head reproduction of the earlier analysis because the corpus, time coverage, preprocessing, leakage controls, feature construction, splitting protocol, and class-handling strategy differ.

Any comparison should therefore be described as a methodological comparison. The revised framework provides stronger controls against duplicate-content leakage, author overlap, preprocessing leakage, artificial test balancing, and post-test model selection.

Consequently, differences in numerical performance between the earlier and revised experiments cannot be attributed solely to the choice of classifier.

---

## Figures

### Figure 1
Final independent test performance comparison.

`figures/figure_1_final_test_performance.png`

### Figure 2
Independent test performance with author-cluster bootstrap 95% confidence intervals.

`figures/figure_2_test_confidence_intervals.png`

### Figure 3
Shortcut-term robustness analysis on the validation set.

`figures/figure_3_shortcut_robustness.png`

### Figure 4
Validation-to-test generalization comparison.

`figures/figure_4_validation_test_generalization.png`

---

## Final Experimental Lock

The independent test set has already been evaluated and the results are locked.

No subsequent:

- hyperparameter tuning,
- threshold optimization,
- feature selection,
- vectorizer refitting,
- model switching, or
- model-development decisions

may be justified using the test results.

The primary model therefore remains the pre-test frozen Linear SVM, while Logistic Regression remains the frozen secondary model.