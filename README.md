# Fraud-Detection
# PROBELM OVERVIEW 
  In today’s digital economy, mobile money transactions have become an essential financial service, especially in developing regions where traditional banking infrastructure is limited. However, the growing volume of digital payments has also led to a rise in fraudulent activities, such as unauthorized transfers and cash-out scams. These fraudulent transactions not only cause financial losses but also erode customer trust in mobile payment systems.

The PaySim dataset simulates real-world mobile money transactions to help identify fraudulent behavior patterns. The core problem is a binary classification task: determining whether a given transaction is fraudulent (1) or legitimate (0) based on its features such as transaction type, amount, balances, and user IDs.
# 1. DATASET AND IMPORTS 

 - Dataset: https://www.kaggle.com/datasets/ealaxi/paysim1

 - The PaySim dataset is a synthetic set of financial transaction records generated to simulate mobile money transactions and to support fraud detection research. The typical task is supervised classification: predict whether a transaction is fraudulent (isFraud) given transaction features (amount, sender/receiver balances, transaction type, etc.). The dataset is widely used to test anomaly/fraud detection models because it simulates real-world class imbalance and transaction patterns.

- Typical columns you’ll see in the CSV:

   1.tep — discrete time step (unit: hours) in the simulation.
   2.type — transaction type, e.g. PAYMENT, TRANSFER, CASH_OUT, DEBIT, CASH_IN.
   3.amount — transaction amount.
   4.nameOrig — customer id of the originator.
   5.oldbalanceOrg — initial balance of the originator before the transaction.
   6.newbalanceOrig — balance of the originator after the transaction.
   7.nameDest — customer id of the destination.
   8.oldbalanceDest — initial balance of the destination before the transaction.
   9.newbalanceDest — balance of the destination after the transaction.
   10.isFraud — target label (1 for fraud, 0 otherwise).
   11.isFlaggedFraud — indicates flagged fraud (rare; for example very large transfers flagged by the simulator).

- Data is loaded using Pandas, inspected for missing values, validated for consistency, and cleaned for further analysis.



 
