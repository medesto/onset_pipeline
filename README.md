# onset_pipeline

Annotation guidelines and methodological approach for the paper:

Viani N, Botelle R, Kerwin J, Yin L, Patel R, Stewart R, Velupillai S. "When Did It Start? A Natural Language Processing Approach for Determining Disease Onset from Mental Health Text", submitted at KDD 2020.

Pipeline steps:

1) Extract documents first referral documents for patients with a diagnosis of schizophrenia:
- documents written within 3 months of first referral date
- first referral date after 1st Jan 2012
- diagnosis like %f20% or %schizophrenia%

2) Data filtering
- calculate document length and average line length
- calculate number of symptom keywords per document
- calculate number of time expressions per document
- apply filters (character length >= 50th percentile, average line length >= 25th percentile, at least 1 symptom keyword, more than 5 time expressions)

3) Manual annotation
- randomly extract patients
- manually annotate documents for onset mentions, with type (psychosis simptom, diagnosis, non-specific) and time information (past anchored, past not anchored, current)

4) NLP development
- divide documents in paragraphs and label paragraphs with 1 (contains a past anchored mention) or 0 (otherwise)
- binary classification problem
- model selection with 5-fold cross validation on training set, experimenting with different features (TF-IDF counts vs. embedding features), and supervised machine learning classifiers (LR, RF and SVM)

5) Patient-level ranked list of likely onset dates
- for each patient, look at all predicted relevant paragraphs
- for each paragraph, extract earliest date or age
- rank dates according to paragraph probability
