# Day 03 — LEFT JOIN Case Study  
## Wallets That Receive ETH But Never Send

### Objective
Identify Ethereum addresses that **received ETH but never sent ETH**.

This helps detect:
- Protocol contracts
- Treasury wallets
- Accumulation / passive wallets

---

### Dataset
- Source: `ethereum.transactions` (Dune Analytics)
- Chain: Ethereum Mainnet

---

### SQL Concept Used
**LEFT JOIN**

Why LEFT JOIN?
- We keep all receiver addresses
- We check if they ever appear as senders
- If sender is `NULL`, they never sent ETH

---

### High-Level Logic
1. Take all transactions with ETH received (`to`)
2. LEFT JOIN against sender addresses (`from`)
3. Filter wallets where sender is `NULL`
4. Count how many times ETH was received

---
### Dune Query
https://dune.com/queries/6449862?utm_source=share&utm_medium=copy&utm_campaign=query

### Key Insights

1. These wallets **only appear as receivers (`to`)** and never as senders (`from`).
2. This behavior is common for:
   - Smart contracts
   - Treasury wallets
   - Long-term accumulation addresses
3. A high `received_tx_count` with zero outgoing transactions suggests
   **non-spending or programmatic wallets**, not retail traders.
4. LEFT JOIN with `NULL` filtering is effective for detecting
   **absence of behavior**, which is a powerful on-chain analysis technique.

### Status
- ✅ Query written
- ✅ Tested on Dune
- ⏳ SQL file to be added
- ⏳ Insights to be documented
