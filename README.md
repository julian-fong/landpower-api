# landpower-api

Main Endpoint: https://www.landpower.ca/api/database

## /propertiesChat/

Columns

`id` : Retrieves a specific row id in the database

`message` : Text containing the message

`user_id` : Retrieves all messages from a specific `user_id`

`property_id` : Retrieves all messages for a specific `property_id`

`date_created` : Datetime like - time and date of the message. Example: "2021-02-9, 01:38:49 pm" or "2021-08-27, 11:57:44 am"

### GET /propertiesChat/

Retrieve property chats in the database. Specify either the `id`, `user_id` or `property_id` parameter or both the `user_id` and `property_id` parameters together to retrieve a specific chat log for a user.

## 📘 `propertiesChat` Path Parameters

| Name         | Type   | In   | Required | Description                | Example URL                    |
|--------------|--------|------|----------|----------------------------|--------------------------------|
| `id`         | string | path | No       | Row ID                     | `/propertiesChat/{id}`         |
| `user_id`    | string | path | No       | User ID for the property   | `/propertiesChat/{user_id}`    |
| `property_id`| string | path | No       | Property ID                | `/propertiesChat/{property_id}`|


#### Response
- `200 OK`: JSON property object
- `400 Bad Request`: if data doesn't exist

Example Result

```json
[
    {
        "id": 1,
        "message": "Hi, is this place available?",
        "date_created": "2025-07-15 12:34:56 pm",
        "property_id": 2,
        "user_id": 3
    }
]
```
### POST /propertiesChat/

Inserts a new row into the database. Requires all parameters `date_created`, `user_id`, `property_id`, and `message` parameter.

## 📘 `propertiesChat` Post Parameters

| Name           | Type   | In   | Required  | Description                |
|----------------|--------|------|-----------|----------------------------|
| `message`      | string | body | Yes       | Message                    |
| `user_id`      | int    | body | Yes       | User ID for the property   |
| `property_id`  | int    | body | Yes       | Property ID                |
| `date_created` | string | body | Yes       | Time and date for message  |

Example Body

```json
{
  "message": "Hi, is this place available?",
  "date_created": "2025-07-15 12:34:56",
  "property_id": "2",
  "user_id": "3"
}
```

### PUT /propertiesChat/

Updates a specific row into the database. Requires at least one parameters `date_created`, `user_id`, `property_id` or `message` parameter along with the specific `id` row to update.

## 📘 `propertiesChat` Put Update Parameters

| Name           | Type   | In   | Required | Description                |
|----------------|--------|------|----------|----------------------------|
| `id`           | int    | body | Yes      | id                         |
| `message`      | string | body | No       | Message                    |
| `user_id`      | int    | body | No       | User ID for the property   |
| `property_id`  | int    | body | No       | Property ID                |
| `date_created` | string | body | No       | Time and date for message  |

Example Body

```json
{
  "message": "Hi, is this newer place available?",
  "date_created": "2025-07-15 12:34:56",
  "property_id": "3",
  "user_id": "2",
  "id": 4
}
```

### Delete /propertiesChat/

Deletes a specific row into the database. Requires the specific `id` row or an array of `id`s.

## 📘 `propertiesChat` Put Update Parameters

| Name           | Type   | In   | Required | Description                |
|----------------|--------|------|----------|----------------------------|
| `id`           | int    | body | Yes      | id                         |

Example Body

```json
{
  "id": 1
}

// or

{
  "id": [1, 2, 3]
}
```

## /propertiesManNumbers/

Columns

`id` : Retrieves a specific row id in the database

`company` : Company Name

`address` : Address of the company

`number` : Phone Number

### GET /propertiesManNumbers/

Retrieve property chats in the database. Specify either the `id`, `user_id` or `property_id` parameter or both the `user_id` and `property_id` parameters together to retrieve a specific chat log for a user.

## 📘 `propertiesManNumbers` Path Parameters

| Name         | Type   | In   | Required | Description                | Example URL                      |
|--------------|--------|------|----------|----------------------------|----------------------------------|
| `id`         | string | path | No       | Row ID                     | `/propertiesManNumbers/{id}`     |
| `company`    | string | path | No       | Company Name               | `/propertiesManNumbers/{company}`|
| `address`    | string | path | No       | Address of the company     | `/propertiesManNumbers/{address}`|
| `number`     | string | path | No       | Phone Number of the company| `/propertiesManNumbers/{number}` |


#### Response
- `200 OK`: JSON property object
- `400 Bad Request`: if data doesn't exist

Example Result

```json
[
    {
        "id": 1,
        "message": "Hi, is this place available?",
        "date_created": "2025-07-15 12:34:56 pm",
        "property_id": 2,
        "user_id": 3
    }
]
```
### POST /propertiesManNumbers/

Inserts a new row into the database. Requires at least one of the parameters `company`, `address`, or `number`.

## 📘 `propertiesManNumbers` Post Parameters

| Name           | Type   | In   | Required  | Description                |
|----------------|--------|------|-----------|----------------------------|
| `company`      | string | body | No        | Company Name               |
| `address`      | string | body | No        | Address of the company     |
| `number`       | int    | body | No        | Phone Number of the company|

Example Body

```json
{
    "company": "test123",
    "address": "test"
}
```

### PUT /propertiesManNumbers/

Updates a specific row into the database. Requires at least one parameters `company`, `address`, or `number` parameter along with the specific `id` row to update.

## 📘 `propertiesManNumbers` Put Update Parameters

| Name           | Type   | In   | Required  | Description                |
|----------------|--------|------|-----------|----------------------------|
| `id`           | int    | body | Yes       | id                         |
| `company`      | string | body | No        | Company Name               |
| `address`      | string | body | No        | Address of the company     |
| `number`       | int    | body | No        | Phone Number of the company|

Example Body

```json
{
    "number": "12345678",
    "id": 1
}
```

### Delete /propertiesManNumbers/

Deletes a specific row into the database. Requires the specific `id` row or an array of `id`s.

## 📘 `propertiesManNumbers` Put Update Parameters

| Name           | Type   | In   | Required | Description                |
|----------------|--------|------|----------|----------------------------|
| `id`           | int    | body | Yes      | id                         |

Example Body

```json
{
  "id": 1
}

// or

{
  "id": [1, 2, 3]
}
```

## /propertiesSchedule/

Columns

- `id` : Unique identifier for each schedule
- `title` : Title of the schedule
- `startTime` : Start time of the schedule
- `endTime` : End time of the schedule
- `technician`, `tenant`, `landlord`, `agent` : Flags indicating role (1 or 0)
- `technicians_id` : ID of the assigned technician
- `property_id` : ID of the associated property

---

### GET /propertiesSchedule/

Retrieve schedule data from the database.

- No query parameters: returns all schedule rows.
- With `id`: returns the row with that ID.
- With `property_id`: returns all schedules associated with that property.

#### 📘 Query Parameters

| Name           | Type   | In    | Required | Description                             |
|----------------|--------|-------|----------|-----------------------------------------|
| `id`           | int    | query | No       | Retrieve a specific schedule by ID      |
| `property_id`  | int    | query | No       | Filter schedules by associated property |

#### Example Request

```
GET /propertiesSchedule?id=1
```

#### Example Response

```json
[
    {
        "id": 1,
        "title": "",
        "startTime": "2024-12-26T00:00:00",
        "endTime": "2024-12-27T00:00:00",
        "technician": 0,
        "tenant": 0,
        "landlord": 0,
        "agent": 1,
        "technicians_id": 0,
        "property_id": 2
    }
]
```

#### Responses

- `200 OK`: Success
- `400 Bad Request`: Invalid parameters or no data found

---

### POST /propertiesSchedule/

Insert a new schedule into the database.

Requires:

- `startTime`, `endTime`, `property_id`
- At least one role flag: `technician`, `tenant`, `landlord`, or `agent`

#### 📘 Request Body

| Name             | Type    | Required | Description                         |
|------------------|---------|----------|-------------------------------------|
| `title`          | string  | No       | Title of the schedule               |
| `startTime`      | string  | Yes      | Schedule start time (datetime)      |
| `endTime`        | string  | Yes      | Schedule end time (datetime)        |
| `technician`     | int     | No       | 1 if technician involved            |
| `tenant`         | int     | No       | 1 if tenant involved                |
| `landlord`       | int     | No       | 1 if landlord involved              |
| `agent`          | int     | No       | 1 if agent involved                 |
| `technicians_id` | string  | No       | Technician ID                       |
| `property_id`    | string  | Yes      | Property ID                         |

#### Example Request Body

```json
{
  "title": "HVAC Maintenance",
  "startTime": "2025-07-20 10:00",
  "endTime": "2025-07-20 12:00",
  "technician": 1,
  "technicians_id": "T789",
  "property_id": "P999"
}
```

#### Responses

- `200 OK`: Insert successful
- `400 Bad Request`: Missing or invalid data
- `500 Server Error`: Internal server error

---

### PUT /propertiesSchedule/

Update an existing schedule by ID.

Requires:

- `id`
- At least one field to update

#### 📘 Request Body

| Name             | Type   | Required | Description                         |
|------------------|--------|----------|-------------------------------------|
| `id`             | int    | Yes      | ID of the schedule to update        |
| `title`          | string | No       | Updated title                       |
| `startTime`      | string | No       | Updated start time                  |
| `endTime`        | string | No       | Updated end time                    |
| `technician`     | int    | No       | Updated technician flag             |
| `tenant`         | int    | No       | Updated tenant flag                 |
| `landlord`       | int    | No       | Updated landlord flag               |
| `agent`          | int    | No       | Updated agent flag                  |
| `technicians_id` | string | No       | Updated technician ID               |
| `property_id`    | string | No       | Updated property ID                 |

#### Example Request Body

```json
{
  "id": 1,
  "endTime": "2025-07-15 12:30",
  "agent": 1
}
```

#### Responses

- `200 OK`: Update successful
- `400 Bad Request`: Missing `id` or no fields to update
- `500 Server Error`: Internal error

---

### DELETE /propertiesSchedule/

Delete schedule entries by ID or list of IDs.

#### 📘 Request Body

| Name | Type        | Required | Description                      |
|------|-------------|----------|----------------------------------|
| `id` | int \| int[]| Yes      | ID or array of IDs to be deleted |

#### Example Request Body

Single ID:

```json
{
  "id": 3
}
```

Multiple IDs:

```json
{
  "id": [4, 5, 6]
}
```

#### Responses

- `200 OK`: Deletion successful
- `400 Bad Request`: Invalid or missing IDs
- `500 Server Error`: Internal error


## /propertiesTechnicians/

Handles CRUD operations for property technician entries.

### Table: `propertiesTechnicians`

| Column               | Type    | Description                    |
|----------------------|---------|--------------------------------|
| `id`                 | int     | Primary key                    |
| `url`                | string  | Technician file URL            |
| `name`               | string  | Technician name                |
| `company`            | string  | Technician company             |
| `phone`              | string  | Phone number                   |
| `email`              | string  | Email                          |
| `website`            | string  | Website URL                    |
| `quotation`          | number  | Quotation amount               |
| `offerQuote`         | string  | Offer or quote notes           |
| `scheduleTechnician` | string  | Schedule time/date             |
| `visited`            | int     | 0 or 1                         |
| `property_id`        | string  | Linked property ID             |
| `maintenance_id`     | string  | Linked maintenance ID          |

---

### GET /propertiesTechnicians

Retrieves technician records.

#### Query Parameters

| Parameter        | Type   | Required | Description                      |
|------------------|--------|----------|----------------------------------|
| `id`             | string | No       | Fetch a technician by ID         |
| `property_id`    | string | No       | Filter by property               |
| `maintenance_id` | string | No       | Filter by maintenance job        |

#### Behavior

- No query params: returns all records.
- One of the three params: filtered search.
- Multiple or invalid query params: 400 Bad Request.

#### Example Request

```http
GET /propertiesTechnicians?maintenance_id=MT123
```

#### Example Response

```json
[
  {
    "id": 4,
    "name": "John Doe",
    "company": "Tech Solutions",
    "property_id": "P100",
    "maintenance_id": "MT123"
  }
]
```

---

### POST /propertiesTechnicians

Creates a new technician record.

#### Required Fields

| Field             | Required | Notes                       |
|------------------|----------|------------------------------|
| `url`            | Yes      |                              |
| `property_id`    | Yes      |                              |
| `maintenance_id` | Yes      |                              |

#### Optional Fields

- `name`, `company`, `phone`, `email`, `website`, `quotation`, `offerQuote`, `scheduleTechnician`, `visited`

#### Example Request Body

```json
{
  "url": "https://example.com/file.pdf",
  "name": "Jane Smith",
  "company": "FixIt Inc",
  "phone": "1234567890",
  "property_id": "P200",
  "maintenance_id": "MT456"
}
```

#### Success Response

```json
{ "message": "Insert successful" }
```

#### Error Responses

- `400`: Missing required fields
- `500`: Server/database error

---

### PUT /propertiesTechnicians

Updates a technician record.

#### Request Body Fields

| Field                 | Type    | Required | Description                     |
|----------------------|---------|----------|---------------------------------|
| `id`                 | int     | Yes      | ID of the technician to update  |
| `url`                | string  | No       | Technician file URL             |
| `name`               | string  | No       | Technician name                 |
| `company`            | string  | No       | Technician company              |
| `phone`              | string  | No       | Phone number                    |
| `email`              | string  | No       | Email                           |
| `website`            | string  | No       | Website URL                     |
| `quotation`          | number  | No       | Quotation amount                |
| `offerQuote`         | string  | No       | Offer or quote notes            |
| `scheduleTechnician` | string  | No       | Schedule time/date              |
| `visited`            | int     | No       | 0 or 1                          |
| `property_id`        | string  | No       | Linked property ID              |
| `maintenance_id`     | string  | No       | Linked maintenance ID           |

#### Example Request Body

```json
{
  "id": 3,
  "visited": 1,
  "offerQuote": "Updated quote details",
  "email": "newemail@example.com"
}
```

#### Success Response

```json
{ "message": "Update successful" }
```

#### Error Responses

- `400`: Missing `id`, invalid `id`, or no valid update fields provided
- `500`: Server/database error


### DELETE /propertiesTechnicians

Deletes one or more technician records.

#### Request Body

```json
{ "id": 5 }
```

```json
{ "id": [3, 4, 7] }
```

#### Behavior

- Validates that all `id`s exist before deletion.
- Supports single or batch deletion.

#### Success Response

```json
{ "message": "Deletion successful" }
```

#### Error Responses

- `400`: Missing or invalid `id`, including one non-existent ID
- `500`: Server/database error


## /tenantAppliances/

Handles CRUD operations for tenant appliance records.

### Columns

- `id` (int) – Primary key
- `name` (string)
- `type` (string)
- `details` (string)
- `installed` (date)
- `warranty` (date)
- `notes` (string)
- `date_created` (date)
- `property_id` (string)
- `user_id` (string)

---

### GET /tenantAppliances/

Fetch tenant appliances by specific query parameters.

#### Query Parameters

| Parameter     | Type   | Required | Description                               |
|--------------|--------|----------|-------------------------------------------|
| `id`         | int    | No       | Fetch a specific appliance by ID          |
| `user_id`    | string | No       | Fetch appliances for a specific user      |
| `property_id`| string | No       | Fetch appliances for a specific property  |

#### Rules

- Provide exactly **1** or exactly **2** of the following: `id`, `user_id`, `property_id`.
- If 2 provided, both must be `user_id` and `property_id`.

#### Example Request

```http
GET /tenantAppliances?user_id=123&property_id=456
```

#### Example Response

```json
[
  {
    "id": 3,
    "name": "Washing Machine",
    "type": "Appliance",
    "details": "Samsung 7kg",
    "installed": "2024-05-01",
    "warranty": "2026-05-01",
    "notes": "Installed upstairs",
    "date_created": "2024-04-30",
    "property_id": "P456",
    "user_id": "U123"
  }
]
```

#### Responses

- `400 Bad Request` — If invalid combination or missing parameters
- `400 Data Not Found` — If no record matches

---

### POST /tenantAppliances/

Insert a new appliance record.

#### Required Fields in Body (JSON)

| Field         | Type   | Required | Description               |
|---------------|--------|----------|---------------------------|
| `name`        | string | No       | Appliance name            |
| `type`        | string | No       | Appliance type            |
| `details`     | string | No       | Extra details             |
| `installed`   | string | Yes      | Install date (YYYY-MM-DD) |
| `warranty`    | string | Yes      | Warranty date (YYYY-MM-DD)|
| `notes`       | string | No       | Optional notes            |
| `date_created`| string | Yes      | Creation date             |
| `property_id` | string | Yes      | Associated property ID    |
| `user_id`     | string | Yes      | Associated user ID        |

#### Example Request Body

```json
{
  "name": "Dishwasher",
  "type": "Appliance",
  "details": "Bosch Series 6",
  "installed": "2025-01-10",
  "warranty": "2027-01-10",
  "notes": "Installed in kitchen",
  "date_created": "2025-01-11",
  "property_id": "789",
  "user_id": "321"
}
```

#### Success Response

```json
{ "message": "Insert successful" }
```

#### Errors

- `400` — Missing required fields
- `500` — Database/server error

---

### PUT /tenantAppliances/

Update an existing appliance record by `id`.

#### Required in Body

- `id`: ID of the row to update
- At least one updatable field

#### Updatable Fields

| Field         | Type   | Required | Description               |
|---------------|--------|----------|---------------------------|
| `name`        | string | No       | Appliance name            |
| `type`        | string | No       | Appliance type            |
| `details`     | string | No       | Extra details             |
| `installed`   | string | Yes      | Install date (YYYY-MM-DD) |
| `warranty`    | string | Yes      | Warranty date (YYYY-MM-DD)|
| `notes`       | string | No       | Optional notes            |
| `date_created`| string | Yes      | Creation date             |
| `property_id` | string | Yes      | Associated property ID    |
| `user_id`     | string | Yes      | Associated user ID        |

#### 🧾 Example Request Body

```json
{
  "id": 3,
  "warranty": "2026-12-31",
  "notes": "Warranty extended"
}
```

#### Success Response

```json
{ "message": "Update successful" }
```

#### Errors

- `400` — Missing or invalid `id`, or no fields provided
- `500` — Database error

---

### DELETE /tenantAppliances/

Delete one or more appliance records.

#### Request Body

| Field | Type        | Required | Description                    |
|-------|-------------|----------|--------------------------------|
| `id`  | int \| int[]| Yes      | ID or array of IDs to delete   |

#### Example Request Body

```json
{ "id": 5 }
```

```json
{ "id": [6, 7, 8] }
```

```json
{ "message": "Deletion successful" }
```

#### Errors

- `400` — Invalid or missing ID(s)
- `500` — Database/server error

---
