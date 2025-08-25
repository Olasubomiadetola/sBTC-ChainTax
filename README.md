
#  sBTC-ChainTax: A Smart Contract for Advanced Taxation on Stacks Blockchain

## Overview

**sBTC-ChainTax** is a feature-rich Clarity smart contract for managing **complex tax calculations** in a decentralized system. It supports **progressive income tax brackets**, **multi-currency handling**, **deductions**, and **detailed taxpayer profiling**. Designed for high-compliance and transparency-focused financial systems on the Stacks blockchain.

---

## ✨ Features

* ✅ Progressive tax bracket computation
* 🌍 Multi-currency support with exchange rate conversions
* 💸 Deduction management with approval workflows
* 📁 Detailed taxpayer profiling and transaction history
* 📊 Read-only reporting functions for tax insights and net obligations
* 🔐 Administrator-controlled configuration

---

## 🏛 Data Structures

### `administrator`

* Contract administrator (set to deploying principal)

### `currency-exchange-rates`

Stores exchange rate info:

```clojure
{
  currency-code: string-ascii(10),
  exchange-rate: uint (scaled by 1e8),
  rate-update-timestamp: uint,
  currency-status: bool
}
```

### `income-tax-brackets`

Defines progressive tax brackets per income category:

```clojure
{
  income-category: string-ascii(24),
  tax-brackets: list of {
    income-threshold: uint,
    tax-percentage: uint,
    bracket-description: string-ascii(64)
  },
  base-currency: string-ascii(10),
  bracket-update-timestamp: uint
}
```

### `available-deductions`

Tracks deduction types and configurations:

```clojure
{
  deduction-code: string-ascii(10),
  deduction-name: string-ascii(64),
  maximum-deduction-amount: uint,
  deduction-percentage: uint,
  approval-required: bool
}
```

### `taxpayer-profiles`

Stores individual taxpayer data:

```clojure
{
  cumulative-tax-paid: uint,
  cumulative-tax-refunded: uint,
  most-recent-payment: uint,
  taxpayer-category: string-ascii(24),
  claimed-deductions: list of {
    deduction-code: string-ascii(10),
    deduction-amount: uint,
    deduction-approved: bool
  },
  transaction-history: list of {
    transaction-amount: uint,
    transaction-timestamp: uint,
    transaction-currency: string-ascii(10)
  }
}
```

---

## ⚠️ Error Codes

| Constant                   | Description                                |
| -------------------------- | ------------------------------------------ |
| `ERR-NOT-AUTHORIZED`       | Action attempted by unauthorized principal |
| `ERR-INVALID-AMOUNT`       | Supplied amount is invalid or zero         |
| `ERR-TAX-RATE-NOT-FOUND`   | No tax rate found for category             |
| `ERR-INSUFFICIENT-BALANCE` | Not enough funds to proceed                |
| `ERR-INVALID-TAX-RATE`     | Invalid tax rate parameters                |
| `ERR-INVALID-CURRENCY`     | Currency not recognized                    |
| `ERR-INVALID-DEDUCTION`    | Deduction not found or exceeds limits      |
| `ERR-REFUND-NOT-ALLOWED`   | Refund conditions not met                  |
| `ERR-INVALID-PERIOD`       | Invalid period/tax year                    |
| `ERR-TRANSFER-FAILED`      | Asset transfer failed                      |

---

## 🔒 Private Functions

### `calculate-bracket-tax-amount`

Per-bracket tax logic for progressive income tiers.

### `update-deduction-approval`

Sets the `deduction-approved` flag for a specific claimed deduction.

### `sum-approved-deductions`

Sums only approved deductions for net tax calculations.

---

## 📖 Read-only Functions

### `get-taxpayer-profile`

Returns the taxpayer profile including deductions and payment history.

### `get-currency-rate`

Fetches exchange rate details for a given currency.

### `get-deduction-info`

Provides metadata for a specific deduction code.

### `get-tax-bracket-info`

Retrieves the full bracket structure for an income category.

### `convert-between-currencies`

Converts an amount from source to target currency using stored exchange rates.

### `calculate-progressive-tax`

Calculates owed tax using progressive brackets.

### `generate-annual-tax-report`

Returns a taxpayer’s full report for a given tax year.

### `calculate-net-tax-obligation`

Computes net tax due after accounting for all approved deductions.

---

## ✅ Usage Scenarios

* Government or DAO managing blockchain-native tax system
* Employer integrations for auto-deductions and reports
* DeFi platforms introducing compliance layers
* Financial tools providing audit and reporting

---

## 🧠 Future Enhancements (Ideas)

* Add support for recurring tax periods (monthly/quarterly)
* NFT or token-based proof of tax compliance
* Integration with oracles for real-time currency rates
* On-chain audits and zero-knowledge compliance proofing

---
