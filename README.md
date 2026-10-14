# ValidateEmails - Email Verification API

A powerful and scalable REST API for real-time, batch, and bulk email verification using DNS, MX, and SMTP checks.

---

## Base URL
https://api.validateemails.co/api/v1/

## Authentication

All requests must include the API key:

**Header:**
x-api-key: YOUR_API_KEY

You can create up to **5 custom API keys** with:
- Active / Inactive control
- IP Whitelisting
- Project-level access separation

---

## Verification Types

| Type       | Description                                      |
|------------|--------------------------------------------------|
| Real-Time  | Verify a single email instantly                  |
| Batch      | Verify up to 100 emails in one request           |
| Bulk       | Use the validateemails.co platform to accomplish it |

---

# 1. Real-Time Single Email Verification

### Endpoint
GET /email_verify?email=EMAIL_ADDRESS

### Example Request
```bash
curl -X GET "https://api.validateemails.co/api/v1/email_verify?email=example@example.com" \
  -H "x-api-key: YOUR_API_KEY"
```

### Success Response
```json
{
  "email": "example@example.com",
  "email_status": "valid",
  "advance_status": "Deliverable",
  "domain": "example.com",
  "ai_rationale": "This email address has been confirmed as valid, so you're good to send messages there",
  "smtp_provider": "aspmx.l.google.com",
  "all_mx_records": [
    "aspmx.l.google.com",
    "alt2.aspmx.l.google.com"
  ]
}
```

### Error Response
```json
{
  "error": "Invalid or missing API credentials",
  "status": 401
}
```

---

# 2. Batch Email Verification (Up to 100 Emails)

### Endpoint
POST /batch_email_verify

### Example Request
```bash
curl -X POST "https://api.validateemails.co/api/v1/batch_email_verify" \
  -H "Content-Type: application/json" \
  -H "x-api-key: YOUR_API_KEY" \
  -d '{
        "emails": ["example@example.com", "example2@example.com"]
      }'
```

### Success Response
```json
{
  "results": [
    {
      "email": "example@example.com",
      "email_status": "VALID",
      "advance_status": "Deliverable",
      "domain": "example.com",
      "ai_rationale": "This email address has been confirmed as valid, so you're good to send messages there",
      "smtp_provider": "aspmx.l.google.com",
      "all_mx_records": ["aspmx.l.google.com", "alt2.aspmx.l.google.com"]
    },
    {
      "email": "example2@example.com",
      "email_status": "INVALID",
      "advance_status": "Undeliverable",
      "domain": "example.com",
      "ai_rationale": "This email address doesn't exist, so refrain from sending emails",
      "smtp_provider": "aspmx.l.google.com",
      "all_mx_records": ["aspmx.l.google.com", "alt2.aspmx.l.google.com"]
    }
  ]
}
```

### Error Response
```json
{
  "error": "Invalid or missing API credentials",
  "status": 401
}
```

---

# Error Codes

| Code | Meaning                                               |
|------|-------------------------------------------------------|
| 200  | Success                                               |
| 400  | Invalid request format                                |
| 401  | Invalid or missing API credentials                    |
| 402  | Insufficient credits                                  |
| 403  | Invalid or inactive API key                           |
| 429  | Rate limit exceeded                                   |
| 451  | Access restricted                                     |
| 500  | Internal server error                                 |
| 502  | Email verification unavailable                        |

---

# Notes & Best Practices

- Ensure your account has **enough credits**
- Always whitelist IPs for production
- Batch request supports **2–100 emails**
- SMTP verification time depends on mail server response

---

# Support

For technical assistance:

support@validateemails.co

---

© 2025 ValidateEmails. All Rights Reserved.
