# User Entity

## Overview

The User entity represents individuals who have accounts with the banking system. Each user can own multiple accounts and is uniquely identified in the system.

## Attributes

- **id**: Unique identifier for the user (UUID)
- **username**: User's login identifier
- **email**: User's email address
- **firstName**: User's first name
- **lastName**: User's last name
- **dateOfBirth**: User's date of birth
- **phoneNumber**: User's contact phone number
- **address**: User's physical address
- **createdAt**: Date when the user record was created
- **updatedAt**: Date when the user record was last updated

## Relationships

- Has many **Accounts**

## Security Notes

- User authentication is managed through the Auth API
- Personally identifiable information (PII) must be handled according to data protection regulations
- Password storage is handled separately from the user profile data
