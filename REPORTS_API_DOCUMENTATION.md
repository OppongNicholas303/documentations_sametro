# Paymaster Reports API Documentation

## Overview
This document provides comprehensive request/response examples for all reporting endpoints in the Paymaster backend system.

---

## 1. Financial Reports

### 1.1 Transaction Summary Report
**Endpoint:** `GET /api/v1/reports/financial/transactions/summary/`

**Authentication:** JWT Token (Admin, Customer, or Merchant)

**Query Parameters:**
```
start_date=2026-02-06 (required)
end_date=2026-02-18 (required)
currency=GHS (optional)
status=Success (optional)
payment_method=Wallet (optional)
transaction_type=pay_order (optional)
channel=app (optional)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/reports/financial/transactions/summary/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "summary": {
        "total_count": 7,
        "total_volume": 2479.68,
        "average_value": 354.24
    },
    "success_rate": 85.71,
    "by_status": [
        {
            "status": "Success",
            "count": 6,
            "amount": 2107.68
        },
        {
            "status": "Pending",
            "count": 1,
            "amount": 372.0
        }
    ],
    "by_payment_method": [
        {
            "payment_method": "Wallet",
            "count": 6,
            "amount": 2107.68
        },
        {
            "payment_method": "Mobile Money",
            "count": 1,
            "amount": 372.0
        }
    ],
    "by_transaction_type": [
        {
            "transaction_type": "pay_order",
            "count": 5,
            "amount": 1680.0
        }
    ],
    "by_channel": [
        {
            "channel": "app",
            "count": 7,
            "amount": 2479.68
        }
    ]
}
```

---

### 1.2 Revenue Report
**Endpoint:** `GET /api/v1/reports/financial/revenue/`

**Authentication:** JWT Token (Merchant or Admin)

**Query Parameters:**
```
start_date=2026-02-06 (required)
end_date=2026-02-18 (required)
currency=GHS (optional)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/reports/financial/revenue/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "revenue_summary": {
        "total_revenue": 673.89,
        "currency": "GHS",
        "orders_count": 2,
        "unique_customers": 2,
        "average_order_value": 336.945
    },
    "revenue_trend": [
        {
            "date": "2026-02-18",
            "revenue": 673.89,
            "orders": 2
        }
    ],
    "top_customers": [
        {
            "payer__first_name": "John",
            "payer__last_name": "Doe",
            "payer__username": "customer1",
            "total_spent": 406.93,
            "orders": 1
        },
        {
            "payer__first_name": "Jane",
            "payer__last_name": "Smith",
            "payer__username": "customer2",
            "total_spent": 266.96,
            "orders": 1
        }
    ]
}
```

---

### 1.3 Payment Methods Report
**Endpoint:** `GET /api/v1/reports/financial/payment-methods/`

**Authentication:** JWT Token (Admin, Customer, or Merchant)

**Query Parameters:**
```
start_date=2026-02-06 (required)
end_date=2026-02-18 (required)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/reports/financial/payment-methods/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "summary": {
        "total_transactions": 6,
        "total_volume": 2107.68
    },
    "payment_methods": [
        {
            "payment_method": "Wallet",
            "count": 6,
            "volume": 2107.68,
            "percentage": 100.0,
            "average_value": 351.28
        }
    ]
}
```

---

### 1.4 Currency Report
**Endpoint:** `GET /api/v1/reports/financial/currencies/`

**Authentication:** JWT Token (Admin, Customer, or Merchant)

**Query Parameters:**
```
start_date=2026-02-06 (required)
end_date=2026-02-18 (required)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/reports/financial/currencies/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06",
        "end_date": "2026-02-18"
    },
    "currencies": [
        {
            "currency": "GHS",
            "count": 6,
            "volume": 2107.68,
            "percentage": 100.0
        }
    ],
    "total_transactions": 6,
    "base_currency": "GHS"
}
```

---

### 1.5 Failed Transactions Report
**Endpoint:** `GET /api/v1/reports/financial/failed-transactions/`

**Authentication:** JWT Token (Admin, Customer, or Merchant)

**Query Parameters:**
```
start_date=2026-02-06 (required)
end_date=2026-02-18 (required)
payment_method=Wallet (optional)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/reports/financial/failed-transactions/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "summary": {
        "total_failed_transactions": 1,
        "total_failed_amount": 372.0,
        "failure_rate": 14.29
    },
    "failed_transactions": [
        {
            "id": "uuid-here",
            "amount": 372.0,
            "currency": "GHS",
            "payment_method": "Mobile Money",
            "transaction_type": "wallet_topup",
            "payer": "customer3",
            "payee": null,
            "created_at": "2026-02-18T12:09:25Z",
            "description": "Withdrawal failed"
        }
    ],
    "by_payment_method": [
        {
            "payment_method": "Mobile Money",
            "count": 1,
            "amount": 372.0
        }
    ]
}
```

---

### 1.6 Reconciliation Report
**Endpoint:** `GET /api/v1/reports/financial/reconciliation/`

**Authentication:** JWT Token (Admin, Customer, or Merchant)

**Query Parameters:**
```
start_date=2026-02-06 (required)
end_date=2026-02-18 (required)
account_type=Wallet (optional) 
currency=GHS (optional)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/reports/financial/reconciliation/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "reconciliation": {
        "total_credits": 1708.69,
        "total_debits": 1708.69,
        "net_change": 0.0,
        "currency": "GHS",
        "transaction_count": 6,
        "ledger_entries_count": 0
    },
    "by_account_type": [
        {
            "account_type": "Wallet",
            "credits": 1708.69,
            "debits": 1708.69,
            "net": 0.0
        }
    ],
    "discrepancies": []
}
```

---

## 2. Merchant Reports

### 2.1 Sales Performance
**Endpoint:** `GET /api/v1/auth/reports/merchant/sales-performance/`

**Authentication:** JWT Token (Merchant only)

**Query Parameters:**
```
start_date=2026-02-06 (required)
end_date=2026-02-18 (required)
store_id=uuid (optional)
group_by=day|week|month (optional, default: day)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/auth/reports/merchant/sales-performance/?start_date=2026-02-06&end_date=2026-02-18&group_by=day
Authorization: Bearer <MERCHANT_JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z",
        "group_by": "day"
    },
    "summary": {
        "total_revenue": 673.89,
        "total_transactions": 2,
        "average_transaction": 336.945,
        "growth_rate": 0.0
    },
    "sales_trend": [
        {
            "period": "2026-02-18",
            "revenue": 673.89,
            "transactions": 2,
            "average_value": 336.945,
            "unique_customers": 2
        }
    ]
}
```

---

### 2.2 Customer Acquisition
**Endpoint:** `GET /api/v1/auth/reports/merchant/customer-acquisition/`

**Authentication:** JWT Token (Merchant only)

**Query Parameters:**
```
start_date=2026-02-06 (required)
end_date=2026-02-18 (required)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/auth/reports/merchant/customer-acquisition/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <MERCHANT_JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "summary": {
        "total_customers": 2,
        "new_customers": 2,
        "returning_customers": 0,
        "retention_rate": 0.0
    },
    "new_customers": {
        "count": 2,
        "revenue": 673.89,
        "transactions": 2,
        "avg_value": 336.945
    },
    "returning_customers": {
        "count": 0,
        "revenue": 0.0,
        "transactions": 0,
        "avg_value": 0.0
    },
    "daily_acquisition": [
        {
            "date": "2026-02-18",
            "new_customers": 2,
            "revenue": 673.89
        }
    ],
    "top_customers": [
        {
            "payer__first_name": "John",
            "payer__last_name": "Doe",
            "payer__username": "customer1",
            "total_spent": 406.93,
            "transactions": 1
        }
    ]
}
```

---

### 2.3 Product Performance
**Endpoint:** `GET /api/v1/auth/reports/merchant/product-performance/`

**Authentication:** JWT Token (Merchant only)

**Query Parameters:**
```
start_date=2026-02-06 (required)
end_date=2026-02-18 (required)
store_id=uuid (optional)
limit=10 (optional, default: 10)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/auth/reports/merchant/product-performance/?start_date=2026-02-06&end_date=2026-02-18&limit=10
Authorization: Bearer <MERCHANT_JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "summary": {
        "total_products_sold": 0,
        "total_quantity": 0,
        "total_revenue": 0.0,
        "total_orders": 0
    },
    "top_products": [],
    "category_performance": []
}
```

---

### 2.4 Merchant Dashboard
**Endpoint:** `GET /api/v1/auth/reports/merchant/dashboard/`

**Authentication:** JWT Token (Merchant only)

**Query Parameters:**
```
start_date=2026-02-06 (required)
end_date=2026-02-18 (required)
store_id=uuid (optional)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/auth/reports/merchant/dashboard/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <MERCHANT_JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "key_metrics": {
        "total_revenue": 673.89,
        "total_transactions": 2,
        "unique_customers": 2,
        "average_order_value": 336.945
    },
    "recent_transactions": [
        {
            "id": "uuid",
            "amount": 406.93,
            "currency": "GHS",
            "payer": "customer1",
            "status": "Success",
            "created_at": "2026-02-18T12:09:25Z"
        }
    ]
}
```

---

## 3. Admin Reports

### 3.1 Platform Metrics
**Endpoint:** `GET /api/v1/auth/reports/admin/platform-metrics/`

**Authentication:** JWT Token (Admin only)

**Query Parameters:**
```
start_date=2026-02-06 (required)
end_date=2026-02-18 (required)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/auth/reports/admin/platform-metrics/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <ADMIN_JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "transaction_metrics": {
        "total_transactions": 7,
        "successful_transactions": 6,
        "failed_transactions": 1,
        "total_volume": 2479.68,
        "success_rate": 85.71
    },
    "user_metrics": {
        "total_active_users": 5,
        "new_users": 2,
        "merchants_count": 3,
        "customers_count": 5
    },
    "daily_volume": [
        {
            "date": "2026-02-18",
            "transactions": 7,
            "volume": 2479.68,
            "success_count": 6
        }
    ]
}
```

---

### 3.2 User Growth
**Endpoint:** `GET /api/v1/auth/reports/admin/user-growth/`

**Authentication:** JWT Token (Admin only)

**Query Parameters:**
```
start_date=2026-02-06 (required)
end_date=2026-02-18 (required)
group_by=day|week|month (optional, default: day)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/auth/reports/admin/user-growth/?start_date=2026-02-06&end_date=2026-02-18&group_by=day
Authorization: Bearer <ADMIN_JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06",
        "end_date": "2026-02-18",
        "group_by": "day"
    },
    "new_users": {
        "total": 2,
        "customers": 0,
        "merchants": 0
    },
    "all_time_users": {
        "total": 8,
        "customers": 5,
        "merchants": 3,
        "verified_users": 8
    },
    "active_users": 5,
    "registration_trend": [
        {
            "period": "2026-02-16",
            "total": 2,
            "customers": 0,
            "merchants": 0
        }
    ],
    "by_country": [
        {
            "profile__country": "Ghana",
            "count": 8
        }
    ]
}
```

---

### 3.3 KYC Statistics
**Endpoint:** `GET /api/v1/auth/reports/admin/kyc-statistics/`

**Authentication:** JWT Token (Admin only)

**Query Parameters:**
```
start_date=2026-02-06 (optional)
end_date=2026-02-18 (optional)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/auth/reports/admin/kyc-statistics/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <ADMIN_JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "kyc_metrics": {
        "total_submissions": 2,
        "approved": 2,
        "rejected": 0,
        "pending": 0,
        "auto_verified": 1,
        "approval_rate": 100.0,
        "avg_verification_score": 0.95
    },
    "user_verification": {
        "verified_users": 8,
        "total_users": 8,
        "verification_rate": 100.0
    },
    "by_role": [
        {
            "user__profile__role": "merchant",
            "total": 2,
            "approved": 2,
            "rejected": 0,
            "pending": 0
        }
    ],
    "daily_trend": [
        {
            "date": "2026-02-16",
            "submissions": 2,
            "approved": 2,
            "rejected": 0
        }
    ]
}
```

---

### 3.4 Channel Performance
**Endpoint:** `GET /api/v1/auth/reports/admin/channel-performance/`

**Authentication:** JWT Token (Admin only)

**Query Parameters:**
```
start_date=2026-02-06 (required)
end_date=2026-02-18 (required)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/auth/reports/admin/channel-performance/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <ADMIN_JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "summary": {
        "total_transactions": 7,
        "whatsapp_percentage": 0.0,
        "app_percentage": 100.0
    },
    "channel_metrics": [
        {
            "channel": "app",
            "count": 7,
            "volume": 2479.68,
            "percentage": 100.0,
            "average_value": 354.24
        }
    ],
    "daily_performance": {
        "whatsapp": [],
        "app": [
            {
                "date": "2026-02-18",
                "transactions": 7,
                "volume": 2479.68
            }
        ]
    },
    "type_by_channel": [
        {
            "channel": "app",
            "transaction_type": "pay_order",
            "count": 5,
            "volume": 1680.0
        }
    ],
    "payment_by_channel": [
        {
            "channel": "app",
            "payment_method": "Wallet",
            "count": 6,
            "volume": 2107.68
        }
    ]
}
```

---

## 4. Ledger Reports

### 4.1 Account Balance Summary
**Endpoint:** `GET /api/v1/reports/ledger/account-balances/`

**Authentication:** JWT Token (Any authenticated user)

**Query Parameters:**
```
account_type=Wallet (optional)
currency=GHS (optional)
user_id=uuid (optional)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/reports/ledger/account-balances/?account_type=Wallet&currency=GHS
Authorization: Bearer <JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "summary": {
        "total_balance": 5000.0,
        "currency_breakdown": {
            "GHS": 5000.0
        }
    },
    "accounts": [
        {
            "id": "uuid",
            "user": "merchant1",
            "account_type": "Wallet",
            "balance": 2500.0,
            "currency": "GHS",
            "is_active": true
        }
    ],
    "account_types": [
        {
            "account_type": "Wallet",
            "total_balance": 5000.0,
            "account_count": 3
        }
    ]
}
```

---

### 4.2 Ledger Entry Report
**Endpoint:** `GET /api/v1/reports/ledger/entries/`

**Authentication:** JWT Token (Any authenticated user)

**Query Parameters:**
```
start_date=2026-02-06 (optional)
end_date=2026-02-18 (optional)
account_id=uuid (optional)
entry_type=debit|credit (optional)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/reports/ledger/entries/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "summary": {
        "total_entries": 0,
        "total_debits": 0.0,
        "total_credits": 0.0,
        "net_change": 0.0
    },
    "entries": [],
    "by_entry_type": []
}
```

---

### 4.3 Account Reconciliation
**Endpoint:** `GET /api/v1/reports/ledger/reconciliation/`

**Authentication:** JWT Token (Admin only)

**Query Parameters:**
```
start_date=2026-02-06 (optional)
end_date=2026-02-18 (optional)
account_id=uuid (optional)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/reports/ledger/reconciliation/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <ADMIN_JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "reconciliation_summary": {
        "total_account_entries": 0,
        "total_transaction_entries": 0,
        "discrepancies_found": 0,
        "reconciliation_status": "balanced"
    },
    "accounts": [],
    "discrepancies": []
}
```

---

### 4.4 Audit Trail
**Endpoint:** `GET /api/v1/reports/ledger/audit-trail/`

**Authentication:** JWT Token (Admin only)

**Query Parameters:**
```
start_date=2026-02-06 (optional)
end_date=2026-02-18 (optional)
user_id=uuid (optional)
action=create|update|delete (optional)
```

**Request Example (Postman):**
```
GET http://127.0.0.1:8000/api/v1/reports/ledger/audit-trail/?start_date=2026-02-06&end_date=2026-02-18
Authorization: Bearer <ADMIN_JWT_TOKEN>
```

**Response Example (200 OK):**
```json
{
    "period": {
        "start_date": "2026-02-06T00:00:00Z",
        "end_date": "2026-02-18T23:59:59.999999Z"
    },
    "summary": {
        "total_actions": 15,
        "creates": 5,
        "updates": 8,
        "deletes": 2
    },
    "audit_entries": [
        {
            "id": "uuid",
            "user": "admin1",
            "action": "create",
            "model": "Transaction",
            "object_id": "uuid",
            "description": "Created transaction",
            "timestamp": "2026-02-18T12:09:25Z"
        }
    ],
    "by_action": [
        {
            "action": "create",
            "count": 5
        }
    ]
}
```

---

## Authentication

All endpoints require JWT authentication (except where noted).

### Getting JWT Token

**Endpoint:** `POST /api/v1/auth/login/`

**Request Body:**
```json
{
    "username": "your_username",
    "password": "your_password"
}
```

**Response Example:**
```json
{
    "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
    "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9..."
}
```

Use the `access` token in the `Authorization` header:
```
Authorization: Bearer <access_token>
```

---

## Common Query Parameters

### Date Filters
- **Format:** `YYYY-MM-DD`
- **Required for most endpoints**
- **Max range:** 365 days

### Group By (Trends)
- **day** - Daily breakdown
- **week** - Weekly breakdown
- **month** - Monthly breakdown

### Currency
- **Default:** GHS
- **Format:** 3-letter ISO code (GHS, USD, EUR, etc.)

---

## Error Responses

### 400 Bad Request
```json
{
    "detail": "Invalid date format",
    "code": "parse_error"
}
```

### 401 Unauthorized
```json
{
    "detail": "Authentication credentials were not provided."
}
```

### 403 Forbidden
```json
{
    "detail": "You do not have permission to perform this action."
}
```

### 404 Not Found
```json
{
    "detail": "Not found."
}
```

### 500 Server Error
```json
{
    "detail": "Internal server error"
}
```

---

## Rate Limiting
- **Limit:** 1000 requests per hour per user
- **Header:** `X-RateLimit-Remaining`

---

## Caching
- Reports are cached for **5 minutes (300 seconds)**
- Cache is automatically invalidated when data changes
- Add `?nocache=true` to bypass cache (if enabled)

---

## Export (Future)

**Endpoint:** `POST /api/v1/reports/export/`

**Request Body:**
```json
{
    "report_type": "revenue",
    "format": "csv|pdf|excel",
    "filters": {
        "start_date": "2026-02-06",
        "end_date": "2026-02-18"
    }
}
```

---

## Support

For issues or questions, contact: support@paymaster.app
