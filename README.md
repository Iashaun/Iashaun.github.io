# Cross Lingual Innformation Retrieval


## Team Members: 
Shaun Noronha, Sheroz Shaikh

## Background and Motivation
Our proposed tool is designed to perform cross-lingual information retrieval by extracting
relevant documents from a large corpus. It operates based on user-specified queries that can be
provided in any of the seven selected languages: Arabic (Ar), Bengali (Bn), Finnish (Fi),
Japanese (Ja), Korean (Ko), Russian (Ru), and Telugu (Te). Notably, the tool is capable of
retrieving the most relevant top-k documents regardless of the language in which the query is
expressed. This feature obviates the need for machine translation (MT) to translate the query,
which can sometimes hinder retrieval performance. The tool empowers users to effortlessly
access relevant documents in multiple languages, streamlining the information retrieval process
thus avoiding potential issues related to translation quality and ambiguity.

## Dataset
### The Hewlett Foundation Data
We used the data available on [XOR-TyDi]https://nlp.cs.washington.edu/xorqa/

<p align="middle">
  <img src="Images/essay_overview.png" width="450" />
  <img src="Images/promtps.png" width="450" /> 
</p>

### Columns

| Column |Description|
|-------|--------|
| essay_set | 1-8, an id for each set of essays |
| essay | The ascii text of a student's response |
| rater1 domain1 | Rater 1's domain 1 score |
| rater2 domain2 | Rater 2's domain 1 score |
| domain1_score |  Resolved score between the raters; all essays have this | 

## Exploratory Data Analysis

### Essay Set Distribution 

Essays are not equally distributed in the dataset. Different essay sets have different number of essays available. 

The scores for each prompt have different scoring criteria. Minimum and Maximum score that can be graded for each essay is different.

<p align="middle">
  <img src="Images/essay_boxplot.png" width="450" />
  <img src="Images/essay_pie.png" width="450" /> 
</p>


## Implementation

Since we are using a Dataset from a kaggle competition, we were unable to to get the true Y values for the test data. We split the trainng data as follows to get the training and test data.

**Training Data** 80% of the Data.
**Test Data** 20% of the Data.


### Embedding + LSTM
The LSTM method utilizes Word2Vec to convert the essays into word embeddings. These vectors are then sent through an LSTM-based model which assigns it a final score. The model summary can be seen below:
<p align="middle">
  <img src="LSTM/Screenshots/Model Summary.png" width="450" /> 
</p>

This model is then trained using a 5-fold Cross-Validation technique, and the average Kappa is calculated.

The results for this procedure are seen below:
<p align="middle">
  <img src="LSTM/Screenshots/Final Result.png" width="450" />
</p>

### Annoy

Annoy (Approximate Nearest Neighbors Something Something) is a C++ library with Python bindings to search for points in space that are close to a given query point. It also creates large read-only file-based data structures that are mmapped into memory so that many processes may share the same data.

#### Model Design
<p align="middle">
  <img src="Images/flowchart.png" />
</p>

Following Quadratic Weighted Kappa was obtained - 

<p align="middle">
  <img src="Images/results.png" />
</p>


## Conclusion

1. LSTM model performed better than the BERT model. 
2. Quadratic Weighted Kappa of LSTM was higher than that of BERT Model. The higher the kappa value, the better model’s prediction aligns with human-graded scores
3. Further optimizations in our hyperparameters or architecture in BERT Model could lead better results.
4. Bert was trained for 100 epochs, training for higher numbers of epochs could also lead to better results.

| | LSTM | Bert |
|-------|--------|--------|
| Quadratic Weighted Kappa | 0.94 | 0.6615 |


## GitHub Repository -  

Here is the link for the [repository](https://github.com/Iashaun/Iashaun.github.io-Cross-Lingual-Information-Retrieval-CLIR-)

) 

### References
We took inspiration from the following papers and worked on out project

1. Shengyao Z., Linjun S., Guido Z. (2023). Augmenting Passage Representations with Query Generation for
Enhanced Cross-Lingual Dense Retrieval. SIGIR (2023), https://doi.org/10.48550/arXiv.2305.03950
2. Zhuolin J., El-Jaroudi A., William H., Damianos K., Lingjun Z. (2020). Cross-lingual Information Retrieval with
BERT. https://doi.org/10.48550/arXiv.2004.13005
3. Yulong Li, Martin Franz, Md Arafat Sultan, Bhavani Iyer, Young-Suk Lee, Avirup Sil (2022). Learning
Cross-Lingual IR from an English Retriever. NAACL (2022), https://doi.org/10.48550/arXiv.2112.08185
