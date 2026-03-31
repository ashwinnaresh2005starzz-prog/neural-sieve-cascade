# Project Overview

## Title
Neural Sieve Cascade (NSC): Multi-Sieve Deep Learning Pipeline for Malicious URL Detection

## Problem
Malicious URLs are widely used in phishing, malware delivery, credential theft, and defacement attacks. Traditional blacklist and rule-based systems struggle with newly generated, obfuscated, or adversarial URLs. A useful detection system must therefore be both fast and accurate.

## Proposed Solution
Neural Sieve Cascade (NSC) is a confidence-driven three-stage URL classification pipeline that progressively filters URLs through lightweight and deeper models.

Instead of running every URL through an expensive transformer, NSC routes URLs through:

1. **Sieve-1:** Logistic Regression with TF-IDF  
2. **Sieve-2:** CNN + LSTM + BiLSTM soft-voting ensemble  
3. **Sieve-3:** TinyBERT for the hardest cases  

This design improves real-time feasibility while maintaining strong final classification performance.

## Architecture

### Sieve-1
- Character-level TF-IDF features
- Logistic Regression classifier
- Fast lexical screening
- Accepts prediction when confidence >= 0.90

### Sieve-2
- CNN for local lexical patterns
- LSTM for sequential token dependencies
- BiLSTM for bidirectional context
- Soft voting combines all three models
- Accepts prediction when confidence >= 0.90

### Sieve-3
- TinyBERT transformer
- Handles ambiguous and adversarial URLs
- Final resolver for low-confidence samples

## Classes
The system performs four-class classification:
- benign
- defacement
- malware
- phishing

## Key Design Idea
Most URLs do not need the heaviest model. NSC resolves easy cases early and reserves deeper models for harder cases. This reduces unnecessary compute while preserving high overall detection quality.

## Outcome
The final pipeline achieved strong multi-class malicious URL detection performance while remaining more practical than a single-stage heavy-model approach.