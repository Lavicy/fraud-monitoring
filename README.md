# Fraud monitoring

During my bank internship, I came across situations involving fraudulent transfers. This made me interested in looking at transaction data more closely: which types of payment have a higher proportion of fraud, and what should we look at when monitoring changes in activity?

For this project, I used the public PaySim dataset rather than bank or customer records.

The dataset contains about 6.4 million simulated mobile-money transactions. Each record includes a transaction type, amount, time step and fraud label. I focused on summarising and comparing these records using Python, pandas and Matplotlib. The analysis is in [fraud_analysis.ipynb](fraud_analysis.ipynb).

## How I approached the analysis

I started with four columns: time, payment type, amount and fraud label. The first checks look for missing values, negative amounts and labels other than 0 or 1.

Next, I grouped the records by payment type and compared both fraud counts and fraud rates. This matters because the payment types have very different numbers of transactions. Comparing counts alone would give an incomplete picture.

For transaction amounts, I compared the mean and median and plotted the distributions for fraud and non-fraud records. Using both measures helps show whether a few large payments are pulling the average upwards. The histogram uses a log scale transformation to make large and small amounts easier to compare.

The notebook also groups the hourly records into simulation days and plots transaction counts, fraud percentages and average amounts over time. It then breaks down the complete day with the highest fraud percentage by payment type. The idea is to move from an overall pattern to a smaller group of records that can be examined more closely. Days with fewer than 24 observed hours are left out of the trend charts.

## What I found

There are **8,213 fraud-labelled records out of 6,362,620 transactions**, or about **0.129%**. All of these fraud records fall under TRANSFER and CASH_OUT in this dataset.

| Payment type | Total transactions | Fraud records | Fraud rate |
|---|---:|---:|---:|
| TRANSFER | 532,909 | 4,097 | 0.769% |
| CASH_OUT | 2,237,500 | 4,116 | 0.184% |

The clearest finding is that these two types have almost the same number of fraud records, but very different fraud rates. TRANSFER has about **4.2 times the fraud rate** of CASH_OUT. Expressed per 10,000 transactions, that is roughly **77 fraud records for TRANSFER compared with 18 for CASH_OUT**.

This is why I would look at rates alongside counts when comparing payment types. CASH_OUT has slightly more fraud records, but a much larger volume of transactions. The same reasoning applies to daily monitoring: if a percentage rises, it is worth checking whether fraud counts increased or total transaction counts fell.

The main outcome is a clearer comparison of where fraud labels are concentrated in this dataset, together with a notebook for examining changes in activity. These are simulated payments, so the findings do not establish how a real bank would perform. Transaction amounts also do not tell us the final financial loss.

## Run it

Use Python 3.10 or newer. Download the CSV following [data/README.md](data/README.md), then run these commands from the project folder:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m notebook fraud_analysis.ipynb
```

On Windows, activate with `.venv\Scripts\activate`. Run the notebook cells in order and allow a few GB of free memory.
