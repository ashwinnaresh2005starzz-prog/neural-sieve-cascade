# Results Summary

## Evaluation Goal
The goal of this project was to evaluate whether a staged multi-sieve pipeline could improve malicious URL detection efficiency while maintaining high classification performance across four classes:
- benign
- defacement
- malware
- phishing

## Stage-wise Accuracy

| Stage | Model | Accuracy |
|---|---|---:|
| Sieve-1 | Logistic Regression + TF-IDF | 99.00% |
| Sieve-2 | CNN / LSTM / BiLSTM Voting | 91.37% |
| Sieve-3 | TinyBERT | 94.86% |
| Final Pipeline | Neural Sieve Cascade | 97.92% |

## Final Class-wise Metrics

| Class | Precision | Recall | F1-score |
|---|---:|---:|---:|
| Benign | 97% | 99% | 98% |
| Defacement | 99% | 99% | 99% |
| Malware | 99% | 93% | 96% |
| Phishing | 95% | 87% | 91% |

## Interpretation

### Sieve-1
This stage acts as a very fast lexical filter. It is useful for quickly resolving obvious URLs with low computational cost.

### Sieve-2
The ensemble improves robustness by combining local pattern learning and sequential context modeling:
- CNN captures local lexical distortions
- LSTM captures token order and sequence structure
- BiLSTM improves contextual sequence understanding

### Sieve-3
TinyBERT handles the hardest URLs, especially those requiring richer contextual interpretation or adversarial robustness.

## Why the pipeline matters
The main value of NSC is not just the final accuracy. Its real contribution is the confidence-based staged routing logic, which avoids running expensive models on every URL.

## Key Takeaways
- Final pipeline accuracy reached 97.92%
- The staged architecture improved practical efficiency
- The pipeline reduced false negatives for phishing and malware compared to standalone models
- The workflow supports real-time oriented malicious URL screening

## Visual Assets in This Repository
- workflow diagram
- accuracy comparison
- confusion matrix
- precision comparison
- recall comparison
- F1-score comparison