# Deanonymising the Kucoin hacker

This repository contains the data and code I used for this post identifying the
September 2020 Kucoin hacker's withdrawal addresses from Tornado Cash.

I used Google BigQuery to obtain the data in `data/TC\ transactions.csv`. The
SQL was:

```sql
SELECT
  *
FROM `bigquery-public-data.crypto_ethereum.transactions`
WHERE
  (
    to_address="0x12d66f87a04a9e220743712ce6d9bb1b5616b8fc" OR
    to_address="0x47ce0c6ed5b0ce3d3a51fdb1c52dc66a7c3c2936" OR
    to_address="0x910cbd523d972eb0a6f4cae4618ad62622b39dbf" OR
    to_address="0xa160cdab225685da1d56aa342ad8841c3b53f291"
  )
AND (input LIKE "0xb214faa5%" OR input LIKE "0x21a0adb6%")
AND receipt_status=1
ORDER BY to_address, block_number, from_address, nonce
```

To run the Jupyter Notebook, clone this repository and run:

```bash
virtualenv venv
source venv/bin/activate
pip3 install -r requirements.txt
jupyter notebook
```
