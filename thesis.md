# Master's Thesis Project: LETF Adoption and Behavioral Biases

## Project Overview

This project investigates the gap between the strong backtested performance of systematic Leveraged ETF (LETF) strategies and their relatively low adoption for long-term investment. The core hypothesis is that behavioral biases explain this under-adoption more than rational concerns about volatility decay and tail risk.

## Research Question

**To what extent can the relatively low adoption of long-term systematic leveraged ETF strategies be attributed to quantifiable behavioral biases, such as myopic loss aversion and negative sentiment, versus rational concerns over volatility decay, tail risk, and regime-dependent performance?**

## Hypotheses

- **H₀ (Null):** Under-adoption is primarily driven by rational concerns (volatility decay, tail risk, regime-dependent performance)
- **Hₐ (Alternative):** Under-adoption is primarily driven by behavioral biases (myopic loss aversion, fear, gambling framing)

## Key Concepts and Definitions

### Financial Concepts
- **Leveraged ETFs (LETFs):** Funds seeking to return a multiple (2x or 3x) of the daily performance of an underlying index through daily rebalancing
- **Volatility Decay:** Path-dependent mathematical drag on LETF performance in volatile, sideways markets
- **Systematic LETF Strategies:**
  1. Leverage for the Long Run (200-day SMA)
  2. HFEA (Hedgefundie's Excellent Adventure)
  3. Buy and Hold

### Behavioral Concepts
- **Myopic Loss Aversion (MLA):** Tendency to be more sensitive to losses than gains and evaluate portfolios frequently
- **Framing/Priming:** The word "leverage" itself may trigger fear responses despite comparable or lower risk versus single stocks
- **Regime-Dependent Bias:** Recency bias and overfitting to post-2009 bull market performance

## Three-Phase Coding Approach

### Phase 1: Performance Backtesting
**Objective:** Establish the empirical foundation showing strong historical risk-adjusted returns of systematic LETF strategies.

**Output:** Performance tables, charts, and statistical evidence for the literature review.

### Phase 2: NLP Discourse Classification
**Objective:** Quantify the prevalence of behavioral vs. rational discourse about LETFs using a validated LLM-based approach.

**Method:**
1.  **Scraping:** Collect a large corpus of comments from `r/Bogleheads`, `r/ETFs`, `r/investing`
- The Keyword List for posts in the broad subreddits: 
[ 'UPRO', 'TQQQ', 'SSO', 'QLD', 'TMF', 'DBPG', '3EUL', '3QQQ',
  'leveraged etf', 'letf', 'volatility decay', 'leverage for the long run',
  'HFEA', '2x SMA', '3x SMA', '9sig', '200d SMA', 'leverage rotation', 'daily leveraged']
If a post has one of the above keywords, we retrieve comments and replies underneath.
2.  **Prompt Engineering:** Develop a robust few-shot prompt for an LLM (e.g., GPT-4) to classify comments into categories: `Rationally Positive`, `Rationally negative`, `Behaviorally positive`, `Behaviorally negative`, and `Irrelevant/ambigious`.
3.  **Automated Classification:** Process the entire dataset via the LLM API to generate initial labels.
4.  **Manual Verification:** Manually review and correct the labels on a statistically significant random sample of the LLM's classifications to calculate and report the model's accuracy. This human-verified dataset serves as the final ground truth for the analysis.

**Output:** A fully labeled dataset of investor comments, classifier accuracy metrics, and frequency distributions of discourse categories.

### Phase 3: Regression Analysis
**Objective:** Test whether the quantified behavioral discourse is a statistically significant predictor of LETF adoption (net fund flows), while controlling for rational market factors.

**Output:** Multivariate regression tables, coefficient plots, and statistical evidence for hypothesis testing.

## Expected Findings

**Key Hypothesis:** The primary barrier to LETF adoption is psychological framing. On `r/Bogleheads` etc., discourse is expected to be dominated by `Behaviorally negative` classifications. 

**Contrast Hypothesis:** Discourse around other high-risk assets (e.g., sector-specific ETFs) will show significantly less `Behaviorally negative` language than LETF discourse, supporting the "priming" effect hypothesis.

**Regression Hypothesis:** The "Behavioral Fear Index" (volume of `Behaviorally negative` comments) will have a statistically significant negative coefficient on net fund flows, even after controlling for performance and market volatility.

## Code Organization Structure
```
letf-thesis/
├── data/
│   ├── raw/
│   │   ├── price_data/
│   │   ├── reddit_data/
│   │   └── fund_flows/
│   ├── processed/
│   │   └── classified_reddit_data.csv
│   └── results/
├── notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_backtest_analysis.ipynb
│   ├── 03_llm_classification.ipynb
│   ├── 04_regression_analysis.ipynb
├── prompts/
│   └── classification_prompt.txt
├── outputs/
│   ├── figures/
│   └── tables/
├── src/
│   ├── backtest/
│   ├── nlp/
│   └── regression/
├── thesis.md
```

## Key Metrics to Report

### Performance Analysis
- CAGR comparison (LETF strategies vs. benchmarks)
- Risk-adjusted returns (Sharpe, Sortino, Calmar)
- Maximum drawdown and recovery time
- Beta to market indices

### Sentiment Analysis
- Percentage distribution of classification categories (`Rational`, `Behavioral`, etc.) per subreddit.
- **LLM Classifier Accuracy:** Report precision, recall, and F1-score based on the manually verified sample.
- **Manual Correction Rate:** The percentage of LLM labels that required human correction.
- Temporal trends in discourse categories.

### Regression Analysis
- Beta coefficients with confidence intervals
- R² and adjusted R²
- P-values for hypothesis testing
- Model diagnostics (VIF, residual plots)
- Robustness checks across specifications


## Critical Reminders for Coding Tasks

1. **Data Integrity:** Always validate data quality, handle missing values appropriately, and document data sources
2. **Statistical Rigor:** Report confidence intervals, conduct robustness checks, and test assumptions
3. **Visualization Quality:** Create publication-ready figures with proper labels, legends, and captions
4. **Documentation:** Comment code thoroughly, especially complex NLP and statistical procedures
5. **Ethical Considerations:** Respect API rate limits and cite data sources
6. **API & Cost Management:** Monitor API usage and costs during the classification phase. Document the specific LLM version used for reproducibility.


## Literature Review Integration

All quantitative results should tie back to:
- **Rational Agent Theory:** Expected utility, volatility decay models, tail risk literature
- **Behavioral Finance:** Prospect theory, myopic loss aversion, framing effects
- **Sentiment Literature:** NLP in finance, social media and market outcomes
- **ETF Literature:** LETF mechanics, historical performance studies, adoption patterns

---

**Note:** This document called thesis.md and especially the Code Organization Structure should be referenced at the start of every coding session to maintain focus and consistency across the multi-phase analysis.