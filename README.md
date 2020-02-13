# onset_pipeline

Annotation guidelines and methodological approach for the paper:

Viani N, Botelle R, Kerwin J, Yin L, Patel R, Stewart R, Velupillai S. "When Did It Start? A Natural Language Processing Approach for Determining Disease Onset from Mental Health Text", submitted at KDD 2020.

Pipeline steps:

1) Data extraction
Extract documents first referral documents for patients with a diagnosis of schizophrenia:
- documents written within 3 months of first referral date
- diagnosis like %f20% or %schizophrenia%

2) Data filtering
- calculate document length and average line length
- calculate number of symptom keywords per document
- calculate number of time expressions per document
- apply filters (length>= 50th percentile, average line length >= 25th percentile, at least 1 symptom keyword, more than 5 time expressions)

3) Manual annotation
- randomly extract patients
- manually annotate documents for onset mentions, with type (psychosis simptom, diagnosis, non-specific) and time information (past anchored, past not anchored, current)

4) NLP development
- divide documents in paragraphs and label paragraphs with 1 (contains a past anchored mention) or 0 (otherwise)
- cross validation on training set (TF-IDF vs embedding features, LR, RF and SVM)

5) define patient-level ranked list of likely onset dates
- for each patient, look at all predicted relevant paragraphs
- for each paragraph, extract earliest date or age
- rank dates according to paragraph probability
