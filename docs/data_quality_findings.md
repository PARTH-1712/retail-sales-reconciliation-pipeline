# Data Quality Findings

| # | Issue | Rows affected | Decision in Silver |
|---|---|---|---|
| 1 | Missing customer_id | 243,007 (22.8%) | Keep, map to Unknown customer (-1) |
| 2 | Non-product stock codes (POST, DOT, M, C2, C3, D, S, BANK CHARGES, ADJUST, ADJUST2, AMAZONFEE, CRUK, TEST001/2, B, GIFT, gift_0001_*) | about 5,913 | Reject, `NON_PRODUCT_CODE`, explicit list |
| 3 | Price <= 0 | 6,202 zero + 5 negative | Reject, `INVALID_PRICE` |
| 4 | Negative qty on non-C invoices | 3,457 | Reject, `STOCK_ADJUSTMENT` |
| 5 | C invoice with positive qty | 1 | Reject, `CANCELLATION_POSITIVE_QTY` |
| 6 | File overlap, 1 to 9 Dec 2010 | 22,523 rows, 1,088 invoices, 0 differences | Reject file-1 copy, `OVERLAP_DUPLICATE` |
| 7 | Duplicates inside one file | 12,133 extra rows (raw) | Keep and flag |
| 8 | Messy text (`m`, `47503J `) | a few rows | Upper-case and trim |
| 9 | Invoice prefix A (bad debt adjustments) | 5 | Rejected via code `B` |