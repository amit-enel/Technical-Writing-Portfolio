# EV Charging Stations API Documentation

**Base URL:** "https://api.evcharging.mockapi.io/api/v1"

**Resource:** stations

This API manages EV charging station records and provides complete CRUD operations for charging stations.

## Authentication

This is a mock API created for demonstration purposes, so no authentication is required.

## Data Model

### Charging Station Object

| Field | Type | Description |
|---------|---------|-------------|
| id | string | Unique identifier (auto-generated) |
| stationName | string | Name of the charging station |
| location | string | Station location |
| status | string | Current station status |
| connectorCount | number | Number of charging connectors |
| createdAt | string | Record creation timestamp |

---

## Endpoints Overview

| Method | Endpoint | Description |
|----------|------------|-------------|
| GET | /stations | Fetch all charging stations |
| GET | /stations/{id} | Fetch a single charging station |
| POST | /stations | Create a new charging station |
| PUT | /stations/{id} | Replace charging station data |
| PATCH | /stations/{id} | Update charging station partially |
| DELETE | /stations/{id} | Delete a charging station |

---

# API Endpoints

## Get All Charging Stations

**GET** /stations

**Description**

Fetches a list of all charging stations.

### Request

```http
GET /stations
```

### Response (200 OK)

```json
[
  {
    "createdAt": "2026-10-19T08:30:15.457Z",
    "stationName": "Mumbai Central EV Hub",
    "location": "Mumbai",
    "status": "Available",
    "connectorCount": 8,
    "id": "1"
  }
]
```

---

## Get Single Charging Station

**GET** /stations/{id}

**Description**

Fetches a specific charging station by ID.

### Path Parameters

| Parameter | Type | Required | Description |
|------------|--------|----------|-------------|
| id | string | Yes | Charging station ID |

### Request

```http
GET /stations/1
```

### Response (200 OK)

```json
{
  "createdAt": "2026-10-19T08:30:15.457Z",
  "stationName": "Mumbai Central EV Hub",
  "location": "Mumbai",
  "status": "Available",
  "connectorCount": 8,
  "id": "1"
}
```

---

## Create Charging Station

**POST** /stations

**Description**

Creates a new charging station record.

### Request Body

```json
{
  "stationName": "Pune EV Plaza",
  "location": "Pune",
  "status": "Available",
  "connectorCount": 6
}
```

### Response (201 Created)

```json
{
  "createdAt": "2026-10-19T12:15:36.686Z",
  "stationName": "Pune EV Plaza",
  "location": "Pune",
  "status": "Available",
  "connectorCount": 6,
  "id": "41"
}
```

---

## Update Charging Station (Full Update)

**PUT** /stations/{id}

**Description**

Replaces the entire charging station record.

### Request

```http
PUT /stations/41
```

### Request Body

```json
{
  "stationName": "Pune Smart Charging Hub",
  "location": "Pune",
  "status": "Busy",
  "connectorCount": 10
}
```

### Response (200 OK)

```json
{
  "createdAt": "2026-10-19T12:15:36.686Z",
  "stationName": "Pune Smart Charging Hub",
  "location": "Pune",
  "status": "Busy",
  "connectorCount": 10,
  "id": "41"
}
```

---

## Update Charging Station (Partial Update)

**PATCH** /stations/{id}

**Description**

Updates specific fields of a charging station.

### Request

```http
PATCH /stations/41
```

### Request Body

```json
{
  "status": "Maintenance"
}
```

### Response (200 OK)

```json
{
  "createdAt": "2026-10-19T12:15:36.686Z",
  "stationName": "Pune Smart Charging Hub",
  "location": "Pune",
  "status": "Maintenance",
  "connectorCount": 10,
  "id": "41"
}
```

---

## Delete Charging Station

**DELETE** /stations/{id}

**Description**

Deletes a charging station record.

### Request

```http
DELETE /stations/41
```

### Response (200 OK)

```json
{
  "createdAt": "2026-10-19T12:15:36.686Z",
  "stationName": "Pune Smart Charging Hub",
  "location": "Pune",
  "status": "Maintenance",
  "connectorCount": 10,
  "id": "41"
}
```

---

# Error Handling

| Status Code | Description |
|-------------|-------------|
| 400 | Bad Request |
| 404 | Charging Station Not Found |
| 500 | Internal Server Error |

### Example Error Response

```json
{
  "error": "Charging station not found"
}
```

---

# Testing the API

You can test all endpoints using:

1. Postman
2. Browser (for GET requests)
3. cURL commands
4. Swagger UI

---

# Notes

1. This API currently contains sample charging station records.
2. IDs are automatically generated.
3. Charging station status can be:
   - Available
   - Busy
   - Offline
   - Maintenance
4. Since it is a mock API, data persistence may vary depending on the configuration.

---

# Conclusion

This EV Charging Stations API provides complete CRUD functionality for managing charging station records. It allows users to create, view, update, and delete charging station information, making it suitable for EV charging network management applications.