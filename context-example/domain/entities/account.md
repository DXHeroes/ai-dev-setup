# Account Entity

## Overview

The Account entity represents financial accounts held by users in the banking system. Each account is owned by a user and can have multiple transactions associated with it.

## Attributes

- **id**: Unique identifier for the account (UUID)
- **accountNumber**: Unique account number in the banking system
- **type**: Type of account (e.g., Checking, Savings, Investment)
- **balance**: Current balance in the account
- **currency**: Currency of the account (e.g., USD, EUR)
- **status**: Current status of the account (e.g., Active, Frozen, Closed)
- **openedDate**: Date when the account was opened
- **lastActivityDate**: Date of the last activity on the account
- **createdAt**: Date when the account record was created
- **updatedAt**: Date when the account record was last updated

## Relationships

- Belongs to one **User**
- Has many **Transactions**

## Business Rules

- Account balance must always reflect the sum of all processed transactions
- Certain operations may require additional authorization based on account type and amount
- Account status changes must be logged and may trigger notifications
- Some account types may have minimum balance requirements or transaction limits
