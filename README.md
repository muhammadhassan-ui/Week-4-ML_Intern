# Tax Document Summarization Evaluation
## Extractive vs. Abstractive Summarization

## 1. Project Overview

This project evaluates two text summarization approaches on Pakistani tax-related legal documents: extractive summarization using TextRank and abstractive summarization using a Large Language Model (LLM).

The objective is to compare both approaches using human evaluation and automatic metrics. The evaluation focuses on faithfulness, coverage, readability, ROUGE scores, and BERTScore.

## 2. Documents Evaluated

Seven tax-related documents were included:

1. Income Tax Ordinance, 2001
2. Sales Tax Act, 1990
3. Federal Excise Act, 2005
4. Customs Act, 1969
5. Income Tax Rules, 2002
6. Sales Tax Rules, 2006
7. Federal Tax Ombudsman Ordinance, 2000

Summaries were generated from selected excerpts of these PDF documents rather than from every page of each complete document.

## 3. Tools and Technologies

- **Python:** Main programming language.
- **Jupyter Notebook:** Environment for implementation and evaluation.
- **Visual Studio Code:** Development environment.
- **PyPDF:** Extracting text from PDF documents.
- **TextRank:** Extractive summarization.
- **Google Gen AI SDK and Gemini:** Abstractive summarization.
- **ROUGE:** Measuring word and phrase overlap between generated and reference summaries.
- **BERTScore:** Measuring semantic similarity between generated and reference summaries.
- **Pandas:** Data processing and evaluation tables.
- **Matplotlib:** Creating charts and visualizing results.

## 4. Methodology

### 4.1 Extractive Summarization

TextRank was used to identify and select important sentences from each document excerpt. The method reuses sentences from the original text rather than generating entirely new sentences.

**Advantages:**
- Preserves original wording.
- Can reduce the risk of introducing new facts.
- Does not require a generative language model.

**Limitations:**
- Sentences may lack context.
- Outputs can be fragmented or difficult to read.
- Important information may be omitted.

### 4.2 Abstractive Summarization

Gemini was used to generate summaries using a fixed prompt. The prompt instructed the model to produce exactly five sentences in clear English, preserve important legal provisions and obligations, avoid unsupported facts, and avoid guessing when information was unclear.

**Advantages:**
- Produces fluent, readable summaries.
- Can combine related information.
- Can explain complex material more concisely.

**Limitations:**
- May introduce unsupported information.
- Can omit important legal details.
- Requires verification against the original source.

### 4.3 Human Evaluation

Each summary was evaluated on a scale of 1 to 5 using three criteria:

- **Faithfulness:** How accurately the summary represents the original document.
- **Coverage:** How much important information the summary includes.
- **Readability:** How clear and easy the summary is to understand.

The overall human score was calculated as the mean of these three criteria.

### 4.4 Automatic Evaluation

The following metrics were calculated for both summarization methods:

- **ROUGE-1:** Measures unigram overlap.
- **ROUGE-2:** Measures bigram overlap.
- **ROUGE-L:** Measures the longest common subsequence.
- **BERTScore F1:** Estimates semantic similarity using contextual language representations.

Automatic metrics complement human evaluation but cannot independently confirm legal accuracy.

## 5. Results

### 5.1 Average Evaluation Scores

| Evaluation Metric | Abstractive | Extractive |
|---|---:|---:|
| Human Faithfulness | 3.000 | 3.714 |
| Human Coverage | 3.857 | 3.429 |
| Human Readability | 5.000 | 2.000 |
| Overall Human Score | 3.952 | 3.048 |
| ROUGE-1 | 0.351 | 0.138 |
| ROUGE-2 | 0.094 | 0.035 |
| ROUGE-L | 0.216 | 0.093 |
| BERTScore F1 | 0.860 | 0.801 |

### 5.2 Human Evaluation Chart

The following chart compares the average human evaluation scores of both approaches.

![Human Evaluation Comparison](human_evaluation_chart.png)

**Chart interpretation:** Abstractive summaries received higher average coverage and readability scores. Extractive summaries received a higher average faithfulness score in the preliminary evaluation.

To generate this chart in the notebook, use:

```python
import matplotlib.pyplot as plt

human_avg[["faithfulness", "coverage", "readability"]].plot(
    kind="bar",
    figsize=(9, 5)
)

plt.title("Human Evaluation: Extractive vs Abstractive")
plt.xlabel("Summarization Method")
plt.ylabel("Average Score (1–5)")
plt.ylim(0, 5)
plt.xticks(rotation=0)
plt.tight_layout()
plt.savefig("human_evaluation_chart.png", dpi=150, bbox_inches="tight")
plt.show()
```

Keep the resulting `human_evaluation_chart.png` file in the same folder as this README so the image displays correctly on GitHub.

## 6. Key Findings

1. Abstractive summarization achieved a higher average overall human score.
2. Abstractive summaries were rated more readable than extractive summaries.
3. Abstractive summaries received a higher average coverage score.
4. Extractive summaries received a higher average faithfulness score in the preliminary human evaluation.
5. All four automatic metrics had higher average scores for the abstractive method in this experiment.
6. Higher ROUGE or BERTScore values do not guarantee that a summary is factually correct or legally reliable.

## 7. Metric-versus-Human Disagreement Analysis

The notebook identified five candidate cases for further investigation:

| Document | Method | Possible Explanation |
|---|---|---|
| Income Tax Ordinance, 2001 | Extractive | Text fragments may overlap with reference wording but remain difficult to read. |
| Customs Act, 1969 | Extractive | Useful legal content may receive a lower ROUGE score when its wording differs from the reference. |
| Sales Tax Rules, 2006 | Abstractive | Strong word overlap may not guarantee complete coverage or factual accuracy. |
| Federal Excise Act, 2005 | Extractive | Matching legal terms does not necessarily produce a coherent summary. |
| Income Tax Rules, 2002 | Extractive | Selected sentences may contain relevant terms but lack sufficient context. |

These explanations are preliminary hypotheses. Each case must be checked against the original PDF excerpt and reference summary before being treated as a confirmed disagreement.

## 8. Decisions and Limitations

- Seven documents were evaluated, producing 14 summaries: seven extractive and seven abstractive.
- The assignment target of ten summaries per method has not yet been met.
- Summaries were generated from selected PDF excerpts rather than the complete documents.
- Reference summaries may not align precisely with the source excerpts. This can affect ROUGE and BERTScore results.
- Human scores are preliminary and should be verified against the original text.
- The evaluation uses a small dataset, so the findings should not be generalized to all tax documents.
- Legal summaries require careful verification because even a fluent summary may omit or misrepresent a legal obligation.

## 9. Future Improvements

1. Expand the evaluation to at least ten summaries per method.
2. Create accurate reference summaries aligned with each exact source excerpt.
3. Verify faithfulness scores against the original documents.
4. Manually investigate and document at least five confirmed metric-versus-human disagreement cases.
5. Recalculate automatic metrics after improving the reference summaries.
6. Use a second reviewer to improve the consistency of human scoring.
7. Evaluate whether the summaries preserve legal requirements, exceptions, dates, and numerical thresholds.

## 10. Final Conclusion

This project compared TextRank-based extractive summarization with Gemini-based abstractive summarization on seven Pakistani tax-related legal documents. The results showed that abstractive summarization achieved higher average readability, coverage, overall human evaluation, ROUGE scores, and BERTScore F1. Extractive summarization received a higher average faithfulness score in the preliminary human evaluation.

These findings suggest that abstractive summarization can produce clearer and more comprehensive summaries, while extractive summarization can preserve original wording more directly. However, automatic metrics measure overlap or semantic similarity rather than legal correctness.

The results remain preliminary because the dataset contains only seven documents, the reference summaries may not fully match the selected excerpts, and the human scores require verification. Future work should expand the dataset, improve reference summaries, and investigate metric-versus-human disagreements in detail.

**For tax and legal documents, every summary should be checked against the original source before it is used for decision-making or relied upon as legal guidance.**