# Dataset

Download **Synthetic Financial Datasets For Fraud Detection (PaySim)** from [Kaggle](https://www.kaggle.com/datasets/ealaxi/paysim1/data), following its access and licence terms.

Extract the CSV into this folder as:

```text
data/PS_20174392719_1491204439457_log.csv
```

The notebook reads four columns:
- `step`: simulated hour.
- `type`: payment type.
- `amount`: transaction amount in dataset currency units.
- `isFraud`: fraud label (1 or 0).

These are simulated mobile-money transactions, not real customer records. Balance columns are not used because the publisher warns that simulation behaviour affects them. The CSV stays local and is excluded from Git.
