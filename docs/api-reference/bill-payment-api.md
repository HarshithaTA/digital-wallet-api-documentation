
# Bill Payment API Reference

## 1. Overview

The Bill Payment API demonstrates how a client application
can retrieve electricity bill details using a service identifier.

This document describes the proposed endpoint, request format,
response structure, validation rules, and possible error responses.

**API version:** 1.0.0  
**HTTP method:** POST  
**Endpoint:** `/api/v1/bills/fetch`  
**Content type:** `application/json`  
**Authentication:** Bearer token (proposed contract)

> This is a fictional API specification created for a
> technical writing portfolio. It is not a live service.

## 2. Prerequisites

Before making a request, the client must:

- Have a valid access token for the intended environment.
- Know the supported electricity provider identifier.
- Have a valid service identifier.
- Send the request using JSON.

## 3. Request

### Endpoint

`POST /api/v1/bills/fetch`

### Headers

| Header | Required | Description |
| --- | --- | --- |
| Authorization | Yes | Bearer access token |
| Content-Type | Yes | `application/json` |
| Accept | No | Expected response format, such as `application/json` |

### Request body

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| providerCode | string | Yes | Identifier of the bill provider |
| serviceNumber | string | Yes | Fictional electricity service identifier |

### Example request

```http
POST /api/v1/bills/fetch HTTP/1.1
Host: api.example.com
Authorization: Bearer <access-token>
Content-Type: application/json
Accept: application/json
```

```json
{
  "providerCode": "DEMO_ELECTRICITY",
  "serviceNumber": "DEMO-123456"
}
```

The host and identifiers above are placeholders.
Replace them only when working with an implemented test environment.

## 4. Successful response

**Illustrative status:** `200 OK`

```json
{
  "billReference": "BILL-DEMO-001",
  "serviceNumber": "DEMO-123456",
  "amount": 1250.50,
  "currency": "INR",
  "dueDate": "2026-11-15",
  "status": "UNPAID"
}
```

### Response fields

| Field | Type | Description |
| --- | --- | --- |
| billReference | string | Reference assigned to the retrieved bill |
| serviceNumber | string | Service identifier associated with the bill |
| amount | number | Illustrative payable amount |
| currency | string | Currency code |
| dueDate | string | Due date in YYYY-MM-DD format |
| status | string | Illustrative bill status |

## 5. Error responses

The following responses are proposed examples.
The implemented API must define and validate the actual behaviour.

| HTTP status | Meaning | Suggested client action |
| --- | --- | --- |
| 400 Bad Request | Invalid request format or field value | Correct the request and retry |
| 401 Unauthorized | Missing or invalid authentication | Obtain valid credentials |
| 404 Not Found | Bill or service identifier not found | Verify the identifier |
| 429 Too Many Requests | Request rate limit exceeded | Follow the documented rate-limit policy |
| 500 Internal Server Error | Unexpected server failure | Report the issue and follow the retry policy |

## 6. Validation rules

The proposed contract expects the client to:

- Provide both required fields.
- Use a supported provider code.
- Send a service identifier in the accepted format.
- Supply valid authentication credentials.

Exact field constraints and validation error formats must be
confirmed against the API implementation before production use.

## 7. Security considerations

- Never include real access tokens in documentation examples.
- Do not log passwords, access tokens, or other secrets.
- Use only authorized test environments.
- Follow the service's documented authentication and access policies.

## 8. Testing checklist

- [ ] Submit a valid request.
- [ ] Omit a required field.
- [ ] Submit an invalid service identifier.
- [ ] Test missing or invalid authentication.
- [ ] Verify the documented error responses.
- [ ] Confirm response fields against the implementation.

## 9. Limitations

This document describes an illustrative API contract.
No live endpoint is provided, and the example requests have not
been executed against a running service.

Production documentation must be updated after the API contract
and all response behaviours have been verified.

## 10. Document history

| Version | Change |
| --- | --- |
| 1.0.0 | Initial portfolio draft |
