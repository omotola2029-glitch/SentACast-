# SentACast

**AI-powered sentiment analysis and trend forecasting for e-commerce product reviews, with a human in the loop.**

SentACast combines automated sentiment scoring, human review, and time-series forecasting in a single interactive dashboard. It was built so small and medium e-commerce businesses can understand what customers are saying about their products *and* where that sentiment is headed, without needing a data science team or expensive tooling.

## Why this exists

Most sentiment analysis tools do one thing: classify a review as positive, negative, or neutral, and stop there. That leaves two problems unsolved. First, fully automated models misread sarcasm, mixed emotions, and informal language, and there's no way to catch or correct those errors. Second, even accurate sentiment scores are just a snapshot; they don't tell you whether customer opinion is improving or declining.

SentACast addresses both by pairing a lexicon-based sentiment model with a **human-in-the-loop (HITL)** review step, then feeding the corrected data into a forecasting model to project future sentiment trends.

## How it works

1. **Upload**: Drop in a CSV of customer reviews. The system auto-detects review text, date, and rating columns regardless of source format.
2. **Clean & preprocess**: Duplicates, empty rows, URLs, and noise are stripped automatically; text is normalized for analysis.
3. **Sentiment analysis**: Each review is scored using VADER (Valence Aware Dictionary and sEntiment Reasoner), classifying it as positive, negative, or neutral.
4. **Human-in-the-loop review**: Low-confidence predictions are flagged and surfaced to the user for validation or correction.
5. **Forecasting**: Corrected sentiment data is passed to Prophet, which models trend and seasonality to predict where sentiment is headed.
6. **Reporting**: Results are visualized on an interactive dashboard (sentiment distribution, trend charts, word clouds) and exportable as PDF, Word, or Excel.

## Results

Tested on a 50-review clothing dataset (48 after cleaning):

| Metric | Before HITL | After HITL |
|---|---|---|
| Accuracy | 68.75% | **81.25%** |
| Improvement | N/A | **+18.18%** |

Prophet forecasting on sentiment trends achieved an MAE of 0.4687 and RMSE of 0.4973, meaning predictions deviated by roughly 0.47 on a -1 to 1 sentiment scale, with no significant outliers.

The biggest single finding: human correction of just 6 flagged predictions out of 48 reviews drove the full accuracy gain, confirming that targeted human oversight, not full manual review, is enough to meaningfully improve automated sentiment classification.

## Built with

- **Python 3.8+**
- **VADER** (Sentiment Analysis)
- **Prophet** (Time-series forecasting, Meta/Facebook)
- **Streamlit** (Interactive dashboard)
- **Pandas / NumPy** (Data handling)
- **Plotly / Matplotlib / WordCloud** (Visualization)
- **ReportLab / python-docx / openpyxl** (Report export)

## Running it locally

```bash
git clone https://github.com/omotola2029-glitch/SentACast-.git
cd SentACast-
pip install -r requirements.txt
streamlit run app.py
```

The dashboard opens automatically in your browser. Upload a CSV of reviews (or use the built-in sample dataset) to get started.

## Background

This project was developed as a final year dissertation for a BSc in Computer Science at the National Open University of Nigeria (NOUN). It draws on a systematic literature review of 54 studies across sentiment analysis, time-series forecasting, and human-AI collaboration to ground the system design in established research.

## License

MIT
