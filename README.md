# Blocked Clients API

## Overview

Этот микросервис предоставляет API для управления списком заблокированных клиентов. Он позволяет добавлять клиентов в список блокировки, удалять их из списка и проверять, заблокирован ли конкретный клиент.

## Contact

- **Email**: [valery.verevkina@gmail.com](mailto:valery.verevkina@gmail.com)

## Version

- **API Version**: 1.0

## Base URL

- **Server**: https://tbank.ru

## Tags

- **Blocked clients**: Blocked clients API

## Endpoints

### 1. Unblock Clients

- **POST** `/api/v1/clients/unblock`
  - **Summary**: Unblock clients from the blocked list
  - **Request Body**:
    - Content-Type: `application/json`
    - Schema: [UnblockedClientsDto](#unblockedclientsdto)
  - **Responses**:
    - `204`: Clients successfully unblocked
    - `400`: Invalid request
    - `500`: Service error

### 2. Add to Blocked List

- **POST** `/api/v1/clients/block`
  - **Summary**: Add a list of clients to the blocked list
  - **Request Body**:
    - Content-Type: `application/json`
    - Schema: Array of [AddBlockedClientDto](#addblockedclientdto)
  - **Responses**:
    - `204`: Client successfully added to the blocked list
    - `400`: Invalid request
    - `500`: Service error

### 3. Unblock a Specific Client

- **POST** `/api/v1/client/{clientId}/unblock`
  - **Summary**: Unblock a specific client from the blocked list
  - **Path Parameters**:
    - `clientId`: External ID of the client (required)
  - **Responses**:
    - `204`: Client successfully unblocked
    - `400`: Invalid request
    - `500`: Service error

### 4. Add a Specific Client to Blocked List

- **POST** `/api/v1/client/block`
  - **Summary**: Add a specific client to the blocked list
  - **Request Body**:
    - Content-Type: `application/json`
    - Schema: [AddBlockedClientDto](#addblockedclientdto)
  - **Responses**:
    - `204`: Client successfully added to the blocked list
    - `400`: Invalid request
    - `500`: Service error

### 5. Get Blocked Client Information

- **GET** `/api/v1/blocked-clients/{clientId}`
  - **Summary**: Retrieve information about a blocked client
  - **Path Parameters**:
    - `clientId`: External ID of the client (required)
  - **Responses**:
    - `200`: Client exists in blocked list - Schema: [BlockedClientDto](#blockedclientdto)
    - `400`: Invalid request
    - `404`: Client not found in blocked list
    - `500`: Service error

## Schemas

### ErrorResponse

- **Type**: Object
- **Properties**:
  - `message`: String - Description of the error (e.g., "Ошибка валидации")
  - `code`: String - Error code (e.g., "400F")
  - `uid`: String - Unique identifier for the error (e.g., "a6c8116b-bb22-4322-b2d9-c3e9b8cd24c4")
  - `fatal`: Boolean - Indicates if the error is critical (e.g., false)

### UnblockedClientsDto

- **Type**: Object
- **Required**: `clientIds`
- **Properties**:
  - `clientIds`: Array of strings - External IDs of clients to unblock (e.g., `["2C-FE32WE","2C-FE3SE"]`)

### AddBlockedClientDto

- **Type**: Object
- **Required**: `clientId`, `status`
- **Properties**:
  - `clientId`: String - External ID of the client (e.g., "2C-FE32WE")
  - `status`: String - Reason for blocking the client (e.g., "FRAUD")

### BlockedClientDto

- **Type**: Object
- **Required**: `clientId`, `startDate`, `status`, `typeStatus`
- **Properties**:
  - `clientId`: String - External ID of the client (e.g., "2C-FE32WE")
  - `startDate`: String - Start date of the block (format: date-time)
  - `status`: String - Reason for blocking (e.g., "FRAUD")
  - `typeStatus`: String - Indicates if the client is trustworthy (e.g., "NEGATIVE" or "POSITIVE")
 