# Performance Drop Detector

> Automatically pinpoint which accounts, countries, or channels caused a performance drop — using logistic regression across any combination of dimensions.

---

## What Is This?

When performance drops, finding the cause is easy with one or two campaigns. It becomes a real challenge when your data spans hundreds of countries, accounts, and channels — thousands of possible combinations to investigate.

This notebook solves that problem. It scans all your dimensions at once and ranks which combinations are most likely responsible for the drop. Instead of spending days building pivot tables, you get a clear prioritized list in seconds.

No statistical background required.

Just open **PerformanceDropDetector.ipynb**

---

## How It Works

The script compares two time periods — a **Good** and a **Bad** one — across any dimensions and metrics you choose. It uses logistic regression to score each dimension combination by how strongly it predicts whether a date belongs to the Good or Bad period. The results are visualized as a ranked bar chart so you immediately know where to look first.

It also supports **iterative analysis**: once you identify and remove the dominant cause, you can re-run the script to uncover secondary issues hiding underneath.

---

## Features

- Works with any number of dimensions (country, account, channel, campaign, keyword, etc.)
- Works with any metric (cost, conversions, revenue, ROAS, clicks, etc.)
- Handles large datasets with hundreds of dimension combinations
- Visual output — no need to read raw numbers
- Iterative by design — peel back one issue at a time
- Easy to configure — just label your periods and pick your dimensions

---

## Requirements

- Python 3.8+
- pandas
- scikit-learn
- matplotlib
- seaborn

Install all dependencies with:

```bash
pip install pandas scikit-learn matplotlib seaborn
```

---

## Getting Started

### Option A — Using Anaconda (Recommended for non-developers)

1. Download and install [Anaconda](https://www.anaconda.com/download)
2. Open **Anaconda Navigator** and launch **JupyterLab**
3. Navigate to the folder where you saved this notebook and open it
4. Open an **Anaconda Prompt** and run `pip install pandas scikit-learn matplotlib seaborn`
5. Follow the configuration steps below

### Option B — Using pip

```bash
git clone https://github.com/your-username/performance-drop-detector.git
cd performance-drop-detector
pip install -r requirements.txt
jupyter notebook
```

---

## Usage

### 1. Prepare Your Data

Your CSV file should contain the following columns:

| Column | Description |
|---|---|
| `date` | The date range to compare. Can be day-to-day or month-to-month |
| `country`, `account_id`, `channel`, etc. | The dimensions you want to analyze |
| `impressions`, `clicks`, `cost`, `conversions`, `conv value`, etc. | The metrics you want to compare |

You can include as many dimension and metric columns as needed.

### 2. Label Your Periods

In the configuration cell, define which dates are Good and which are Bad:

```python
period_labels = {
    "2024-01": "Good",
    "2024-02": "Good",
    "2024-03": "Bad",
    "2024-04": "Bad"
}
```

### 3. Choose Dimensions and Metric

```python
dimensions = ["country", "account_id", "channel"]  # add or remove as needed
metric = "conv value"                               # the metric to investigate
```

### 4. Run the Notebook

Click **Kernel → Restart & Run All** from the top menu.

### 5. Read the Results

- Bars pointing toward **Bad** = suspects. Start with the longest ones
- If one dimension dominates the chart, remove it and re-run to find secondary issues

---

## Example

In a sample dataset covering **230 countries**, **161 accounts**, and **13 channels**, the script immediately flagged a single account that had stopped spending across multiple countries as the primary cause of the drop. Re-running after removing it revealed a second underperforming account — something that would have been easy to miss in a manual review.

---

## License

MIT License. Free to use and modify.

---

## Contributing

Pull requests are welcome. If you find a bug or have a feature suggestion, please open an issue.
