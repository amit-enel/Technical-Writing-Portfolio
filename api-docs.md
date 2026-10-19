# EV Charging Management API

## Overview

The EV Charging Management API enables operators to retrieve charging station information and manage charging sessions.

### Base URL

```http
https://api.testevcharging.com/v1
```

### Authentication

All API requests require a Bearer token.

**Header**

```http
Authorization: Bearer <access_token>
```

---

# Get Charging Station Status

Retrieves the current status of a charging station.

## Endpoint

```http
GET /stations/{stationId}/status
```

## Request Headers

| Header | Required | Description |
|----------|----------|-------------|
| Authorization | Yes | Bearer access token |
| Accept | Yes | application/json |

## Path Parameters

| Parameter | Type | Required | Description |
|------------|--------|----------|-------------|
| stationId | string | Yes | Unique identifier of charging station |

## Example Request

```bash
curl --request GET \
'https://api.testevcharging.com/v1/stations/STN001/status' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIs...'
```

## Example Response

```json
{
  "stationId": "STN001",
  "status": "Available",
  "connectorCount": 4,
  "availableConnectors": 3,
  "lastUpdated": "2026-10-19T10:30:00Z"
}
```

## Response Attributes

| Attribute | Type | Description |
|------------|--------|-------------|
| stationId | string | Charging station identifier |
| status | string | Current station status |
| connectorCount | integer | Total number of connectors |
| availableConnectors | integer | Number of available connectors |
| lastUpdated | datetime | Timestamp of latest status update |

## HTTP Status Codes

| Status Code | Description |
|-------------|-------------|
| 200 | Request successful |
| 401 | Unauthorized |
| 404 | Station not found |
| 500 | Internal server error |

---

# Start Charging Session

Driver starts a charging session using an RFID card.

## Endpoint

```http
POST /sessions/start
```

## Request Headers

| Header | Required | Description |
|----------|----------|-------------|
| Authorization | Yes | Bearer access token |
| Content-Type | Yes | application/json |

## Request Body

```json
{
  "stationId": "STN001",
  "connectorId": "CON001",
  "rfidTag": "RF123456789"
}
```

## Request Attributes

| Attribute | Type | Required | Description |
|------------|--------|----------|-------------|
| stationId | string | Yes | Station identifier |
| connectorId | string | Yes | Connector identifier |
| rfidTag | string | Yes | RFID card identifier |

## Example Request

```bash
curl --request POST \
'https://api.testevcharging.com/v1/sessions/start' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIs...' \
--header 'Content-Type: application/json' \
--data '{
  "stationId":"STN001",
  "connectorId":"CON001",
  "rfidTag":"RF123456789"
}'
```

## Example Response

```json
{
  "sessionId": "SES12345",
  "status": "Started",
  "startTime": "2026-10-19T11:00:00Z",
  "powerLimit": 22
}
```

## Response Attributes

| Attribute | Type | Description |
|------------|--------|-------------|
| sessionId | string | Unique session identifier |
| status | string | Session status |
| startTime | datetime | Session start time |
| powerLimit | integer | Maximum charging power in kW |

## HTTP Status Codes

| Status Code | Description |
|-------------|-------------|
| 201 | Session created |
| 400 | Invalid request |
| 401 | Unauthorized |
| 409 | Connector already in use |
| 500 | Internal server error |

---

# Error Response

The API returns standard error messages when a request fails.

## Example Error Response

```json
{
  "errorCode": "AUTH_001",
  "message": "Invalid access token",
  "correlationId": "e521f9b7"
}
```

## Error Attributes

| Attribute | Type | Description |
|------------|--------|-------------|
| errorCode | string | Unique error code |
| message | string | Error description |
| correlationId | string | Identifier used for request tracking |

## Common Error Codes

| Error Code | Description |
|------------|-------------|
| AUTH_001 | Invalid access token |
| AUTH_002 | Expired access token |
| STN_001 | Station not found |
| SES_001 | Session not found |
| CON_001 | Connector unavailable |

---

# Rate Limiting

To ensure service availability, API requests are rate limited.

| Limit | Value |
|---------|---------|
| Requests per minute | 100 |
| Burst limit | 20 |

When the rate limit is exceeded, the API returns:

```http
429 Too Many Requests
```

---

# Contact

For API support, contact:

**Email:** api-support@example.com

**Documentation Version:** 1.0.0

**Last Updated:** October 2026
