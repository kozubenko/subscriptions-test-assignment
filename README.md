# README

# Automatic Subscription Rebilling System

## Description
You need to implement a system for automatic subscription rebilling, which will handle scenarios of insufficient funds on the card. If a payment attempt returns an "insufficient funds" response from the bank, the system should reduce the payment amount and retry (up to 4 times). If the payment is successful but for less than the full amount, the remaining balance should be automatically charged a week later.

Each payment attempt should be made using the `/paymentIntents/create` API, which will emulate the payment gateway.

---

## Task

### 1. Main Rebilling Logic:
- First, try to charge the full subscription amount.
- If the bank responds with "insufficient funds," attempt to charge 75%, 50%, and 25% of the amount.
- A maximum of 4 attempts is allowed for each rebill.

### 2. Partial Rebill:
- If a payment succeeds but not for the full amount, automatically schedule an additional transaction one week later for the remaining balance.

### 3. Using the API to Emulate the Payment Gateway:
Each payment attempt should be processed through the `/paymentIntents/create` API, which will return a successful or failed status depending on the conditions.

#### **API Details:**
**Endpoint:** `POST /paymentIntents/create`

**Request:**
```json
{
  "amount": <amount_to_charge>,
  "subscription_id": <subscription_identifier>
}
```

**Response:**
```json
{
  "status": "success" | "failed" | "insufficient_funds"
}
```

---

## Requirements
- Implement in **Ruby** (without using external libraries for payment API handling).
- The logic should be split into clear methods with appropriate exception handling.
- Rebill results should be logged.

---

