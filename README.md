# landpower-api

Main Endpoint: https://www.landpower.ca/api/database

## Table of Contents

- [login](#login)
- [propertiesChat](#propertiesChat)
- [propertiesManNumbers](#propertiesManNumbers)
- [propertiesSchedule](#propertiesSchedule)
- [propertiesTechnicians](#propertiesTechnicians)
- [propertiesTenant](#propertiesTenant)
- [queryProjects](#queryProjects)
- [register](#register)
- [tenantAppliances](#tenantAppliances)
- [tenantEmailTech](#tenantEmailTech)
- [tenantExpenses](#tenantExpenses)
- [tenantImage](#tenantImage)
- [tenantInsurance](#tenantInsurance)
- [tenantList](#tenantList)
- [tenantInvoice](#tenantInvoice)
- [tenantMaintenance](#tenantMaintenance)
- [tenantPayment](#tenantInvoice)
- [users](#users)

## /login

Main Endpoint use log into the website

### POST /login

| Name           | Type   | In   | Required  | Description                |
|----------------|--------|------|-----------|----------------------------|
| `user_name`      | string | body | No       | Username as registered in database    |
| `user_pass`      | string    | body | Yes       | Password   |
| `user_email`  | string    | body | No       | Email as registered in database              |

Example Body

```json
{
  "user_email": "test@test.com",
  "user_pass": "password123",
}
```

#### Success Response

```json
{ "message": "Successful login" }
```

#### Error Responses

- `400`: User Not Found or Incorrect Password
- `500`: Server/database error

### PUT /login

Use this endpoint to update passwords for users

| Name           | Type   | In   | Required  | Description                |
|----------------|--------|------|-----------|----------------------------|
| `user_name`      | string | body | No       | Username as registered in database                  |
| `user_pass`      | string    | body | Yes       | Password   |
| `user_email`  | string    | body | No       | Email as registered in database              |

Example Body

```json
{
  "user_email": "test@test.com",
  "user_pass": "password123",
}
```

#### Success Response

```json
{ "message": "Update successful" }
```

#### Error Responses

- `400`: username not found in update
- `500`: Server/database error

## /propertiesChat

### Table Schema

| Field            | Type        | Description                      |
|------------------|-------------|----------------------------------|
| id        | int(11)     | Auto-increment primary key       |
| message          | text        | Message content                  |
| date_created     | varchar(50) | Date and time the message was created |
| property_id | int(11)     | Foreign key to a property        |
| user_id     | int(11)     | Foreign key to a user            |

Note: 

`date_created` : Datetime like - time and date of the message. Example: "2021-02-9, 01:38:49 pm" or "2021-08-27, 11:57:44 am"

### GET /propertiesChat/

Retrieve property chats in the database. Specify either the `id`, `user_id` or `property_id` parameter or both the `user_id` and `property_id` parameters together to retrieve a specific chat log for a user.

## `propertiesChat` Path Parameters

| Name         | Type   | In   | Required | Description                | Example URL                    |
|--------------|--------|------|----------|----------------------------|--------------------------------|
| `id`         | int | path | No       | Row ID                     | `/propertiesChat/{id}`         |
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
### POST /propertiesChat

Inserts a new row into the database. Requires all parameters `date_created`, `user_id`, `property_id`, and `message` parameter.

## `propertiesChat` Post Parameters

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

### PUT /propertiesChat

Updates a specific row into the database. Requires at least one parameters `date_created`, `user_id`, `property_id` or `message` parameter along with the specific `id` row to update.

## `propertiesChat` Put Update Parameters

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

### Delete /propertiesChat

Deletes a specific row into the database. Requires the specific `id` row or an array of `id`s.

## `propertiesChat` Put Update Parameters

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

### Table Schema

| Field     | Type          | Description                     |
|-----------|---------------|---------------------------------|
| id | int(11)       | Auto-increment primary key      |
| company   | varchar(255)  | Management name                    |
| address   | varchar(255)  | Management address                 |
| number    | varchar(255)  | Management phone number      |


### GET /propertiesManNumbers/

Retrieve property chats in the database. Specify either the `id`, `user_id` or `property_id` parameter or both the `user_id` and `property_id` parameters together to retrieve a specific chat log for a user.

## `propertiesManNumbers` Path Parameters

| Name         | Type   | In   | Required | Description                | Example URL                      |
|--------------|--------|------|----------|----------------------------|----------------------------------|
| `id`         | int | path | No       | Row ID                     | `/propertiesManNumbers/{id}`     |
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
### POST /propertiesManNumbers

Inserts a new row into the database. Requires at least one of the parameters `company`, `address`, or `number`.

## `propertiesManNumbers` Post Parameters

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

### PUT /propertiesManNumbers

Updates a specific row into the database. Requires at least one parameters `company`, `address`, or `number` parameter along with the specific `id` row to update.

## `propertiesManNumbers` Put Update Parameters

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

### Delete /propertiesManNumbers

Deletes a specific row into the database. Requires the specific `id` row or an array of `id`s.

## `propertiesManNumbers` Put Update Parameters

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

### Table Schema

| Field               | Type          | Description                        |
|---------------------|---------------|----------------------------------|
| id          | int(11)       | Auto-increment primary key        |
| title               | varchar(50)   | Title of the record or event      |
| startTime           | varchar(50)   | Start time (stored as string)     |
| endTime             | varchar(50)   | End time (stored as string)       |
| technician          | int(11)       | Technician ID                     |
| tenant              | int(11)       | Tenant ID                        |
| landlord            | int(11)       | Landlord ID                      |
| agent               | int(11)       | Agent ID                        |
| technicians_id | int(11)       | Index/reference for technician   |
| property_id    | int(11)       | Index/reference for property      |

Note:

`startTime` and `endTime` are of format `YYYY-MM-DDTHH:MM:SS`

---

### GET /propertiesSchedule/

Retrieve schedule data from the database.

- No query parameters: returns all schedule rows.
- With `id`: returns the row with that ID.
- With `property_id`: returns all schedules associated with that property.

#### Query Parameters

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

### POST /propertiesSchedule

Insert a new schedule into the database.

Requires:

- `startTime`, `endTime`, `property_id`
- At least one role flag: `technician`, `tenant`, `landlord`, or `agent`

#### Request Body

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

### PUT /propertiesSchedule

Update an existing schedule by ID.

Requires:

- `id`
- At least one field to update

#### Request Body

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

### DELETE /propertiesSchedule

Delete schedule entries by ID or list of IDs.

#### Request Body

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

### Table Schema:

| Field                | Type          | Description                     |
|----------------------|---------------|---------------------------------|
| id           | int(11)       | Auto-increment primary key      |
| url                  | varchar(255)  | URL associated with the record  |
| name                 | varchar(255)  | Name of the technician or entity|
| company              | varchar(255)  | Company name                   |
| phone                | varchar(50)   | Phone number                   |
| email                | varchar(255)  | Email address                  |
| website              | varchar(255)  | Website URL                    |
| quotation            | int(11)       | Quotation amount (numeric)     |
| offerQuote           | varchar(255)  | Offer or quote description     |
| scheduleTechnician   | varchar(255)  | Technician schedule info       |
| visited              | int(11)       | Visit count or flag            |
| property_id    | int(11)       | Foreign key for property       |
| maintenance_id  | int(11)       | Foreign key for maintenance job|


---

### GET /propertiesTechnicians

Retrieves technician records.

#### Query Parameters

| Parameter        | Type   | Required | Description                      |
|------------------|--------|----------|----------------------------------|
| `id`             | int | No       | Fetch a technician by row ID         |
| `property_id`    | string | No       | Filter by property               |
| `maintenance_id` | string | No       | Filter by maintenance job        |

#### Behavior

- No query params: returns all records.
- One of the three params: filtered search.
- Multiple or invalid query params: 400 Bad Request.

#### Example Request

```http
GET /propertiesTechnicians?maintenance_id=123
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

### GET /propertiesTenant

Retrieves property ids by tenants.

## propertiesTenant Table Schema

| Column Name         | Data Type        | Description                                       |
|---------------------|------------------|---------------------------------------------------|
| id                  | int(11)          | Primary key, auto-incremented ID                  |
| url                 | text             | URL associated with the property                  |
| party_link          | text             | Link to party details                             |
| visited             | int(11)          | Visited status 0/1                                |
| whatsapp            | text             | WhatsApp contact info                             |
| tenant              | text             | Tenant name or ID                                 |
| landlord            | text             | Landlord name or ID                               |
| house_type          | int(11)          | House type code                                   |
| bedroom             | text             | Bedroom description                               |
| bedOther            | text             | Other bed details                                 |
| property            | text             | Property name or description                      |
| address             | text             | Full street address                               |
| unitNumber          | text             | Unit or suite number                              |
| postal_code         | text             | Postal/ZIP code                                   |
| city                | text             | City name                                         |
| cityName            | text             | Alternate city name (if any)                      |
| province            | text             | Province or state                                 |
| propertyTax         | text             | Property tax amount                               |
| maintenanceFee      | text             | Maintenance fee                                   |
| pmNumber            | text             | Property manager phone number                     |
| pmCompany           | text             | Property management company name                  |
| mortgage            | text             | Mortgage amount or status                         |
| propMonthFee        | text             | Monthly property fee                              |
| balance             | text             | Outstanding balance                               |
| phone               | text             | Tenant phone number                               |
| email               | text             | Tenant email address                              |
| rent                | text             | Rent amount                                       |
| lease_starts        | text             | Lease start date                                  |
| lease_ends          | text             | Lease end date                                    |
| rent_type           | text             | Type of rent (e.g., fixed, variable)              |
| type                | text             | General category/type                             |
| credit_score        | text             | Credit score of tenant                            |
| income              | text             | Reported income                                   |
| total_occupants     | text             | Number of people living in the unit               |
| recurring_invoice   | text             | Recurring invoice status/info                     |
| next_invoice        | text             | Date of next invoice                              |
| payment_due         | text             | Payment due date                                  |
| safety_deposit      | text             | Safety deposit amount                             |
| extra_deposit       | text             | Additional deposit amount                         |
| rent_increase       | text             | Upcoming or past rent increase info               |
| policy_number       | text             | Insurance policy number                           |
| notes               | text             | Miscellaneous notes                               |
| background_color    | varchar(50)      | Theme background color                            |
| primary_color       | varchar(50)      | Primary theme color                               |
| second_color        | varchar(50)      | Secondary theme color                             |
| third_color         | varchar(50)      | Tertiary theme color                              |
| text_color          | varchar(50)      | Primary text color                                |
| text_color2         | varchar(50)      | Secondary text color                              |
| background2_color   | varchar(50)      | Additional background color                       |
| background3_color   | varchar(50)      | Another background layer color                    |
| date                | date             | Date associated with the record                   |
| secondary_token     | varchar(255)     | Optional token (e.g., auth/session)               |
| user_id             | int(11)          | Foreign key referencing user                      |
| tenant_id           | int(11)          | Foreign key referencing tenant                    |
| project_id          | int(11)          | Foreign key referencing project                   |
| createdTimestamp    | timestamp        | Timestamp of when record was created              |


#### Query Parameters

| Parameter   | Type   | Required | Description             |
|-------------|--------|----------|-------------------------|
| `id`        | string | No       | Fetch tenant by ID      |
| `user_id`   | string | No       | Fetch tenant by user ID |

#### Behavior

- Only **1** query parameter allowed.
- Allowed parameters: `id`, `user_id`.
- Any other combination returns 400 Bad Request.
- If no data found: returns 400 with message `"Data Not Found"`.

#### Example Request

```http
GET /propertiesTenant?id=123
```

#### Example Response

```json
[
  {
    "id": 123,
    "tenant": "John Doe",
    "address": "123 Main St",
    "email": "john@example.com",
    "phone": "1234567890"
    // ...
  }
]
```

---

### POST /propertiesTenant

Creates a new tenant record.

#### Required Fields

| Field     | Type   | Required | Notes                         |
|-----------|--------|----------|-------------------------------|
| `user_id` | string | Yes      | Owner of the tenant record    |

#### Optional Fields

| Field               | Data Type        |
|---------------------|------------------|
| url                 | text             |
| party_link          | text             |
| visited             | int(11)          |
| whatsapp            | text             |
| tenant              | text             |
| landlord            | text             |
| house_type          | int(11)          |
| bedroom             | text             |
| bedOther            | text             |
| property            | text             |
| address             | text             |
| unitNumber          | text             |
| postal_code         | text             |
| city                | text             |
| cityName            | text             |
| province            | text             |
| propertyTax         | text             |
| maintenanceFee      | text             |
| pmNumber            | text             |
| pmCompany           | text             |
| mortgage            | text             |
| propMonthFee        | text             |
| balance             | text             |
| phone               | text             |
| email               | text             |
| rent                | text             |
| lease_starts        | text             |
| lease_ends          | text             |
| rent_type           | text             |
| type                | text             |
| credit_score        | text             |
| income              | text             |
| total_occupants     | text             |
| recurring_invoice   | text             |
| next_invoice        | text             |
| payment_due         | text             |
| safety_deposit      | text             |
| extra_deposit       | text             |
| rent_increase       | text             |
| policy_number       | text             |
| notes               | text             |
| background_color    | varchar(50)      |
| primary_color       | varchar(50)      |
| second_color        | varchar(50)      |
| third_color         | varchar(50)      |
| text_color          | varchar(50)      |
| text_color2         | varchar(50)      |
| background2_color   | varchar(50)      |
| background3_color   | varchar(50)      |
| date                | date             |
| secondary_token     | varchar(255)     |
| user_id             | int(11)          |
| tenant_id           | int(11)          |
| project_id          | int(11)          |
| createdTimestamp    | timestamp        |

#### Example Request Body

```json
{
  "user_id": "789",
  "tenant": "Jane Smith",
  "email": "jane@example.com",
  "address": "456 Queen St",
  "city": "Toronto"
}
```

#### Success Response

```json
{ "message": "Insert successful" }
```

#### Error Responses

- `400`: Missing `user_id`
- `500`: Server/database error

---

### PUT /propertiesTenant

Updates an existing tenant record.

#### Required Field

| Field | Type   | Required | Description               |
|-------|--------|----------|---------------------------|
| `id`  | string | Yes      | ID of the record to update|

#### Updatable Fields

Same as optional fields from the POST method.

#### Behavior

- Requires a valid existing `id`
- At least one updatable field must be included

#### Example Request Body

```json
{
  "id": 123,
  "email": "newemail@example.com",
  "notes": "Updated tenant notes"
}
```

#### Success Response

```json
{ "message": "Update successful" }
```

#### Error Responses

- `400`: Missing or invalid `id`, or no update fields provided
- `500`: Server/database error

---

### DELETE /propertiesTenant

Deletes one or more tenant records.

#### Request Body

```json
{ "id": 123 }
```

```json
{ "id": [123, 124, 125] }
```

#### Behavior

- Accepts a single `id` or array of IDs
- Validates that all IDs exist before deletion

#### Success Response

```json
{ "message": "Deletion successful" }
```

#### Error Responses

- `400`: Missing or invalid `id`, including one non-existent or invalid type
- `500`: Server/database error

## /queryProjects

Endpoint to retrieve pre-construction project information.

Using this endpoint also retrieves information from other tables such as
- Floorplans
- PriceLists
- Features
- SubImages
- Developers

### /queryProjects/

#### Query Parameters


| Name         | Type   | In   | Required | Description                | Example URL                    |
|--------------|--------|------|----------|----------------------------|--------------------------------|
| `id`         | int | path | No       | Row ID                     | `/queryProjects/{id}`         |
| `projectName`    | string | path | No       | User ID for the property   | `/queryProjects/{projectName}`    |

## /register

Endpoint to insert new users into the database - uses the `users` table

### POST /register

Insert a new appliance record.

#### Required Fields in Body (JSON)

| Field         | Type   | Required | Description               |
|---------------|--------|----------|---------------------------|
| `user_name`        | string | Yes       | username of the account |
| `user_pass`     | string | Yes       | password for the account         |
| `user_email`     | string | Yes       | email of the account         |
| `user_date`     | string | No       |  Date of registration      |
| `user_level`     | string | Yes       | role of the account   |

Note:

`user_date` is of format YYYY-MM-DD HH:MM:SS

## /tenantAppliances

Handles CRUD operations for tenant appliance records.

### Columns

| Field           | Type         | Description                          |
|-----------------|--------------|------------------------------------|
| id    | int(11)      | Auto-increment primary key          |
| name            | varchar(255) | Name of the item                    |
| type            | varchar(255) | Type or category                   |
| details         | varchar(255) | Additional details                  |
| installed       | date         | Installation date                  |
| warranty        | date         | Warranty expiration date           |
| notes           | text         | Notes or comments                  |
| property_id | int(11)      | Foreign key to property             |
| date_created    | date         | Record creation date               |
| user_id    | int(11)      | Foreign key to user                 |

Note:

`date_created` is of format: YYYY-MM-DD

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

### POST /tenantAppliances

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

### PUT /tenantAppliances

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

#### Example Request Body

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

### DELETE /tenantAppliances

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

## /tenantEmailTech/

Handles CRUD operations for tenant email tech records.

### Table Schema:

| Field           | Type         | Description                          |
|-----------------|--------------|--------------------------------------|
| id              | int(11)      | Auto-increment primary key           |
| link            | varchar(255) | Link or URL                         |
| email           | varchar(255) | Email address                       |
| interested      | int(11)      | Interest level or status            |
| property_id     | int(11)      | Foreign key to property             |
| maintenance_id  | int(11)      | Foreign key to maintenance record   |
| user_id         | int(11)      | Foreign key to user                 |
| date_created    | varchar(50)  | Record creation date                |

Note:

`date_created` is of format: YYYY-MM-DD

---

### GET /tenantEmailTech/

Fetch tenant email tech records by specific query parameters.

#### Query Parameters

| Parameter       | Type   | Required | Description                                    |
|-----------------|--------|----------|------------------------------------------------|
| `id`            | int    | No       | Fetch a specific record by ID                  |
| `user_id`       | string | No       | Fetch records for a specific user              |
| `property_id`   | string | No       | Fetch records for a specific property          |
| `maintenance_id`| string | No       | Fetch records for a specific maintenance item  |

#### Rules

- Provide exactly **1** of the following: `id`, `user_id`, `property_id`, or `maintenance_id`.

#### Example Request

```http
GET /tenantEmailTech?user_id=123
```

#### Example Response

```json
[
  {
    "id": 5,
    "link": "https://example.com/tech-support",
    "email": "tenant@example.com",
    "interested": 1,
    "property_id": "456",
    "maintenance_id": "789",
    "user_id": "123",
    "date_created": "2024-04-30"
  }
]
```

#### Responses

- `400 Bad Request` — If invalid combination or missing parameters
- `400 Data Not Found` — If no record matches

---

### POST /tenantEmailTech

Insert a new email tech record.

#### Required Fields in Body (JSON)

| Field           | Type   | Required | Description                       |
|-----------------|--------|----------|-----------------------------------|
| `link`          | string | No       | Link or URL                      |
| `email`         | string | No       | Email address                    |
| `interested`    | int    | No       | Interest level (default: 0)      |
| `property_id`   | string | Yes      | Associated property ID            |
| `maintenance_id`| string | Yes      | Associated maintenance ID         |
| `user_id`       | string | Yes      | Associated user ID                |
| `date_created`  | string | Yes      | Creation date (YYYY-MM-DD)        |

#### Example Request Body

```json
{
  "link": "https://example.com/repair-request",
  "email": "tenant@example.com",
  "interested": 1,
  "property_id": "456",
  "maintenance_id": "789",
  "user_id": "123",
  "date_created": "2025-01-11"
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

### PUT /tenantEmailTech

Update an existing email tech record by `id`.

#### Required in Body

- `id`: ID of the row to update
- At least one updatable field

#### Updatable Fields

| Field           | Type   | Required | Description                       |
|-----------------|--------|----------|-----------------------------------|
| `link`          | string | No       | Link or URL                      |
| `email`         | string | No       | Email address                    |
| `interested`    | int    | No       | Interest level                   |
| `property_id`   | string | No       | Associated property ID            |
| `maintenance_id`| string | No       | Associated maintenance ID         |
| `user_id`       | string | No       | Associated user ID                |
| `date_created`  | string | No       | Creation date (YYYY-MM-DD)        |

#### Example Request Body

```json
{
  "id": 5,
  "interested": 0,
  "email": "updated@example.com"
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

### DELETE /tenantEmailTech

Delete one or more email tech records.

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

#### Success Response

```json
{ "message": "Deletion successful" }
```

#### Errors

- `400` — Invalid or missing ID(s)
- `500` — Database/server error

---


## /tenantExpenses

Handles CRUD operations for tenant expenses records.

### Table Schema:

| Field         | Type      | Description                     |
|---------------|-----------|---------------------------------|
| id            | int(11)   | Auto-increment primary key      |
| category      | text      | Expense category                |
| other_repair  | text      | Other repair description       |
| pay_to        | text      | Payee                          |
| balance       | text      | Balance amount                 |
| status        | text      | Payment status (paid/unpaid)   |
| paid_on       | text      | Date paid (YYYY-MM-DD)         |
| tax_status    | text      | Tax status (yes/no)            |
| rent_invoice  | text      | Rent invoice status (yes/no)   |
| recurring     | text      | Recurring expense (yes/no)     |
| notes         | text      | Additional notes               |
| property_id   | int(11)   | Associated property ID         |
| date_created  | date      | Record creation date (YYYY-MM-DD) |
| user_id       | int(11)   | Associated user ID             |

---

### GET /tenantExpenses/

Fetch tenant expense records by query parameters.

#### Query Parameters

| Parameter     | Type   | Required | Description                             |
|---------------|--------|----------|-----------------------------------------|
| `id`          | int    | No       | Fetch specific record by ID              |
| `user_id`     | int    | No       | Fetch records for a specific user        |
| `property_id` | int    | No       | Fetch records for a specific property    |

#### Rules

- Provide **either** exactly 1 of the parameters (`id`, `user_id`, `property_id`)  
- OR provide **both** `user_id` and `property_id` together.

#### Example Requests

```http
GET /tenantExpenses?id=10
GET /tenantExpenses?user_id=123
GET /tenantExpenses?property_id=456
GET /tenantExpenses?user_id=123&property_id=456
```

#### Example Response

```json
[
  {
    "id": 5,
    "category": "Plumbing",
    "other_repair": "Fixed leaking faucet",
    "pay_to": "Joe's Plumbing",
    "balance": "150.00",
    "status": "paid",
    "paid_on": "2025-06-10",
    "tax_status": "yes",
    "rent_invoice": "no",
    "recurring": "no",
    "notes": "Work done promptly",
    "property_id": "456",
    "date_created": "2025-06-01",
    "user_id": "123"
  }
]
```

#### Responses

- `400 Bad Request` — Invalid or missing parameters
- `400 Data Not Found` — No records matched

---

### POST /tenantExpenses

Insert a new tenant expense record.

#### Required Fields in JSON Body

| Field         | Type   | Required | Description                        |
|---------------|--------|----------|------------------------------------|
| `property_id` | int    | Yes      | Associated property ID              |
| `date_created`| string | Yes      | Record creation date (YYYY-MM-DD)  |
| `user_id`     | int    | Yes      | Associated user ID                  |

#### Optional Fields

| Field         | Type   | Description                        |
|---------------|--------|------------------------------------|
| `category`      | string | Expense category                   |
| `other_repair`  | string | Other repair description          |
| `pay_to`        | string | Payee                            |
| `balance`       | string | Balance amount                   |
| `status`        | string | Payment status (paid/unpaid)     |
| `paid_on`       | string | Date paid (YYYY-MM-DD)           |
| `tax_status`    | string | Tax status (yes/no)              |
| `rent_invoice`  | string | Rent invoice status (yes/no)     |
| `recurring`     | string | Recurring expense (yes/no)       |
| `notes`         | string | Additional notes                 |

#### Example Request Body

```json
{
  "category": "Plumbing",
  "other_repair": "Fixed leaking faucet",
  "pay_to": "Joe's Plumbing",
  "balance": "150.00",
  "status": "paid",
  "paid_on": "2025-06-10",
  "tax_status": "yes",
  "rent_invoice": "no",
  "recurring": "no",
  "notes": "Work done promptly",
  "property_id": 456,
  "date_created": "2025-06-01",
  "user_id": 123
}
```

#### Success Response

```json
{ "message": "Insert successful" }
```

#### Errors

- `400` — Missing required fields
- `500` — Database or server error

---

### PUT /tenantExpenses

Update an existing tenant expense record by `id`.

#### Required in Body

- `id` (int): ID of the record to update  
- At least one updatable field from below.

#### Updatable Fields

| Field         | Type   | Description                        |
|---------------|--------|------------------------------------|
| `category`      | string | Expense category                   |
| `other_repair`  | string | Other repair description          |
| `pay_to`        | string | Payee                            |
| `balance`       | string | Balance amount                   |
| `status`        | string | Payment status (paid/unpaid)     |
| `paid_on`       | string | Date paid (YYYY-MM-DD)           |
| `tax_status`    | string | Tax status (yes/no)              |
| `rent_invoice`  | string | Rent invoice status (yes/no)     |
| `recurring`     | string | Recurring expense (yes/no)       |
| `notes`         | string | Additional notes                 |
| `property_id`   | int    | Associated property ID            |
| `date_created`  | string | Record creation date (YYYY-MM-DD)|
| `user_id`       | int    | Associated user ID                |

#### Example Request Body

```json
{
  "id": 5,
  "status": "unpaid",
  "notes": "Payment pending"
}
```

#### Success Response

```json
{ "message": "Update successful" }
```

#### Errors

- `400` — Missing or invalid `id`, or no fields to update
- `500` — Database error

---

### DELETE /tenantExpenses

Delete one or more tenant expense records.

#### Request Body

| Field | Type       | Required | Description                  |
|-------|------------|----------|------------------------------|
| `id`  | int \| int[] | Yes      | ID or array of IDs to delete |

#### Example Request Body

Single ID:

```json
{ "id": 5 }
```

Multiple IDs:

```json
{ "id": [6, 7, 8] }
```

#### Success Response

```json
{ "message": "Deletion successful" }
```

#### Errors

- `400` — Invalid or missing ID(s)
- `500` — Database/server error

---

## users

### PUT /users

Use this endpoint to update certain fields of an account

Note:

Possible values for the field `user_level` are 

- Super
- Mod
- Agent
- Regular
- Tenant

#### Required in Body

- `id`: ID of the row to update
- At least one updatable field

#### Updatable Fields

| Field           | Type   | Required | Description                       |
|-----------------|--------|----------|-----------------------------------|
| `user_name`     | string | No       | username of the account           |
| `user_pass`     | string | No       | Password of the account           |
| `user_email`    | int    | No       | Email address                     |
| `user_date`     | string | No       | user date of the account          |
| `user_level`    | string | No       | User access                       |

### DELETE /users

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


## /tenantImage/

Handles CRUD operations for tenant image records.

### Table Schema:

| Field           | Type         | Description                                |
|-----------------|--------------|--------------------------------------------|
| idPrimary       | int(11)      | Auto-increment primary key                 |
| image_name      | varchar(255) | Name of the image or file                  |
| document        | int(11)      | 1 if document type, otherwise 0            |
| maintenance     | int(11)      | 1 if maintenance image, otherwise 0        |
| property_image  | int(11)      | 1 if general property image, otherwise 0   |
| date            | varchar(50)  | Date of upload (format: YYYY-MM-DD HH:MM:SS am/pm) |
| property_id     | int(11)      | Foreign key to a property                  |
| user_id         | int(11)      | Foreign key to a user                      |
| maintenance_id  | int(11)      | Foreign key to a maintenance record        |

---

### GET /tenantImage/

Fetch tenant image records by specific query parameters.

#### Query Parameters

| Parameter       | Type   | Required | Description                             |
|-----------------|--------|----------|-----------------------------------------|
| `id`            | int    | No       | Fetch a specific record by ID           |
| `user_id`       | string | No       | Fetch records for a specific user       |
| `property_id`   | string | No       | Fetch records for a specific property   |
| `user_id` + `property_id` | string | No | Fetch records matching both fields      |

#### Rules

- You must provide either:
  - Exactly **1** of `id`, `user_id`, or `property_id`, **or**
  - Both `user_id` and `property_id`

#### Example Request

```http
GET /tenantImage?user_id=123&property_id=456
```

#### Example Response

```json
[
  {
    "id": 7,
    "image_name": "damage1.jpg",
    "document": 0,
    "maintenance": 1,
    "property_image": 0,
    "date": "2025-06-11 02:30:00 pm",
    "property_id": "456",
    "maintenance_id": "789",
    "user_id": "123"
  }
]
```

#### Responses

- `400 Bad Request` — If invalid or missing parameters  
- `400 Data Not Found` — If no record matches

---

### POST /tenantImage

Insert a new tenant image record.

#### Required Fields in Body (JSON)

| Field           | Type   | Required | Description                                 |
|-----------------|--------|----------|---------------------------------------------|
| `image_name`    | string | Yes      | Name of the file                            |
| `date`          | string | Yes      | Upload timestamp (YYYY-MM-DD HH:MM:SS am/pm) |
| `property_id`   | string | Yes      | Associated property ID                      |
| `maintenance_id`| string | Yes      | Associated maintenance ID                   |
| `user_id`       | string | Yes      | Associated user ID                          |
| `document`      | int    | No       | 1 if it's a document (default: 0)           |
| `maintenance`   | int    | No       | 1 if it's for maintenance (default: 0)      |
| `property_image`| int    | No       | 1 if it's a property image (default: 0)     |

#### Validation Rules

- At least one of `document`, `maintenance`, or `property_image` must be set to `1`.

#### Example Request Body

```json
{
  "image_name": "lease-agreement.pdf",
  "document": 1,
  "maintenance": 0,
  "property_image": 0,
  "date": "2025-07-01 10:15:00 am",
  "property_id": "456",
  "maintenance_id": "789",
  "user_id": "123"
}
```

#### Success Response

```json
{ "message": "Insert successful" }
```

#### Errors

- `400` — Missing required fields or no image type specified  
- `500` — Database/server error

---

### PUT /tenantImage

Update an existing tenant image record by `id`.

#### Required in Body

- `id`: ID of the row to update  
- At least one updatable field

#### Updatable Fields

| Field           | Type   | Required | Description                                |
|-----------------|--------|----------|--------------------------------------------|
| `image_name`    | string | No       | Updated name of the image                  |
| `document`      | int    | No       | Set to 1 or 0                              |
| `maintenance`   | int    | No       | Set to 1 or 0                              |
| `property_image`| int    | No       | Set to 1 or 0                              |
| `date`          | string | No       | Updated date/time                          |
| `property_id`   | string | No       | Updated property ID                        |
| `maintenance_id`| string | No       | Updated maintenance ID                     |
| `user_id`       | string | No       | Updated user ID                            |

#### Example Request Body

```json
{
  "id": 7,
  "image_name": "updated_image.png",
  "document": 0
}
```

#### Success Response

```json
{ "message": "Update successful" }
```

#### Errors

- `400` — Missing `id`, invalid `id`, or no updatable fields  
- `500` — Database error

---

### DELETE /tenantImage

Delete one or more image records.

#### Request Body

| Field | Type        | Required | Description                      |
|-------|-------------|----------|----------------------------------|
| `id`  | int \| int[]| Yes      | ID or array of IDs to delete     |

#### Example Request Body

```json
{ "id": 7 }
```

```json
{ "id": [8, 9, 10] }
```

#### Success Response

```json
{ "message": "Deletion successful" }
```

#### Errors

- `400` — Missing or invalid `id`  
- `500` — Database/server error

## /tenantInsurance/

Handles CRUD operations for tenant insurance records.

### Table Schema:

| Field           | Type      | Description                                     |
|-----------------|-----------|-------------------------------------------------|
| idPrimary       | int(11)   | Auto-increment primary key                      |
| balance         | text      | Total balance                                   |
| other_balance   | text      | Any other balance                               |
| policy          | text      | Policy details or number                        |
| status          | text      | Payment status (paid/unpaid)                    |
| renewal         | text      | Renewal date (YYYY-MM-DD)                       |
| recurring       | text      | Indicates if the insurance is recurring (yes/no)|
| pay_to          | text      | Who to pay the insurance to                     |
| insuranceOther  | text      | Additional insurance info (yes/no)              |
| notes           | text      | Additional notes                                |
| property_id     | int(11)   | Foreign key to a property                       |
| user_id         | int(11)   | Foreign key to a user                           |
| tenant_id       | int(11)   | Foreign key to a tenant                         |
| date_created    | date      | Date of creation (format: YYYY-MM-DD)          |

---

### GET /tenantInsurance/

Fetch tenant insurance records by specific query parameters.

#### Query Parameters

| Parameter       | Type   | Required | Description                             |
|-----------------|--------|----------|-----------------------------------------|
| `id`            | int    | No       | Fetch a specific record by ID           |
| `user_id`       | string | No       | Fetch records for a specific user       |
| `property_id`   | string | No       | Fetch records for a specific property   |
| `user_id` + `property_id` | string | No | Fetch records matching both fields      |

#### Rules

- You must provide either:
  - Exactly **1** of `id`, `user_id`, or `property_id`, **or**
  - Both `user_id` and `property_id`

#### Example Request

```http
GET /tenantInsurance?user_id=123&property_id=456
```

#### Example Response

```json
[
  {
    "id": 1,
    "balance": "1200",
    "other_balance": "300",
    "policy": "ABC123",
    "status": "paid",
    "renewal": "2025-12-01",
    "recurring": "yes",
    "pay_to": "XYZ Insurance",
    "insuranceOther": "no",
    "notes": "Annual plan",
    "user_id": "123",
    "property_id": "456",
    "tenant_id": "789",
    "date_created": "2025-06-15"
  }
]
```

#### Responses

- `400 Bad Request` — If invalid or missing parameters  
- `400 Data Not Found` — If no record matches

---

### POST /tenantInsurance

Insert a new tenant insurance record.

#### Required Fields in Body (JSON)

| Field           | Type   | Required | Description                            |
|----------------|--------|----------|----------------------------------------|
| `balance`       | string | No       | Total balance                          |
| `other_balance` | string | No       | Additional balance                     |
| `policy`        | string | No       | Policy details                         |
| `status`        | string | No       | Payment status (paid/unpaid)           |
| `renewal`       | string | No       | Renewal date (YYYY-MM-DD)              |
| `recurring`     | string | No       | Recurring policy (yes/no)              |
| `pay_to`        | string | No       | Payable to                             |
| `insuranceOther`| string | No       | Other insurance flag (yes/no)          |
| `notes`         | string | No       | Additional notes                       |
| `property_id`   | string | Yes      | Associated property ID                 |
| `user_id`       | string | Yes      | Associated user ID                     |
| `tenant_id`     | string | No       | Tenant ID                              |
| `date_created`  | string | Yes      | Creation date (YYYY-MM-DD)             |

#### Example Request Body

```json
{
  "balance": "1200",
  "other_balance": "300",
  "policy": "ABC123",
  "status": "paid",
  "renewal": "2025-12-01",
  "recurring": "yes",
  "pay_to": "XYZ Insurance",
  "insuranceOther": "no",
  "notes": "Annual plan",
  "property_id": "456",
  "user_id": "123",
  "tenant_id": "789",
  "date_created": "2025-06-15"
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

### PUT /tenantInsurance

Update an existing tenant insurance record by `id`.

#### Required in Body

- `id`: ID of the row to update  
- At least one updatable field

#### Updatable Fields

| Field           | Type   | Description                           |
|-----------------|--------|---------------------------------------|
| `balance`       | string | Updated balance                       |
| `other_balance` | string | Updated other balance                 |
| `policy`        | string | Updated policy                        |
| `status`        | string | Updated status                        |
| `renewal`       | string | Updated renewal date (YYYY-MM-DD)     |
| `recurring`     | string | yes/no                                |
| `pay_to`        | string | Updated pay_to value                  |
| `insuranceOther`| string | Updated insuranceOther value          |
| `notes`         | string | Updated notes                         |
| `tenant_id`     | string | Updated tenant ID                     |
| `property_id`   | string | Updated property ID                   |
| `user_id`       | string | Updated user ID                       |
| `date_created`  | string | Updated date                          |

#### Example Request Body

```json
{
  "id": 1,
  "balance": "1500",
  "status": "unpaid"
}
```

#### Success Response

```json
{ "message": "Update successful" }
```

#### Errors

- `400` — Missing `id`, invalid `id`, or no updatable fields  
- `500` — Database error

---

### DELETE /tenantInsurance

Delete one or more insurance records.

#### Request Body

| Field | Type        | Required | Description                      |
|-------|-------------|----------|----------------------------------|
| `id`  | int \| int[]| Yes      | ID or array of IDs to delete     |

#### Example Request Body

```json
{ "id": 1 }
```

```json
{ "id": [2, 3, 4] }
```

#### Success Response

```json
{ "message": "Deletion successful" }
```

#### Errors

- `400` — Missing or invalid `id`  
- `500` — Database/server error


## /tenantInvoice/

Handles CRUD operations for tenant invoice records.

### Table Schema:

| Field               | Type         | Description                                 |
|--------------------|--------------|---------------------------------------------|
| idPrimary           | int(11)      | Auto-increment primary key                  |
| file_name           | varchar(255) | Name of the file                            |
| policy_number       | varchar(255) | Policy number                               |
| address             | varchar(255) | Address associated with the invoice         |
| tenant              | varchar(255) | Tenant name or ID                           |
| payment_for         | varchar(255) | Description of what payment is for          |
| term_type           | varchar(50)  | Term type (e.g., fixed, monthly)            |
| lease_starts        | date         | Lease start date (YYYY-MM-DD)               |
| lease_ends          | date         | Lease end date (YYYY-MM-DD)                 |
| notes               | text         | Additional notes                            |
| amount              | varchar(255) | Invoice amount                              |
| landlord            | varchar(255) | Landlord name or ID                         |
| landlord_signature  | varchar(255) | Signature or agreement confirmation         |
| date                | date         | Date the invoice was created (YYYY-MM-DD)   |
| property_id         | int(11)      | Foreign key to a property                   |
| user_id             | int(11)      | Foreign key to a user                       |

---

### GET /tenantInvoice/

Fetch tenant invoice records by specific query parameters.

#### Query Parameters

| Parameter       | Type   | Required | Description                             |
|-----------------|--------|----------|-----------------------------------------|
| `id`            | int    | No       | Fetch a specific record by ID           |
| `user_id`       | string | No       | Fetch records for a specific user       |
| `property_id`   | string | No       | Fetch records for a specific property   |
| `user_id` + `property_id` | string | No | Fetch records matching both fields      |

#### Rules

- You must provide either:
  - Exactly **1** of `id`, `user_id`, or `property_id`, **or**
  - Both `user_id` and `property_id`

#### Example Request

```http
GET /tenantInvoice?user_id=123&property_id=456
```

#### Responses

- `400 Bad Request` — If invalid or missing parameters  
- `400 Data Not Found` — If no record matches

---

### POST /tenantInvoice

Insert a new tenant invoice record.

#### Required Fields in Body (JSON)

| Field              | Type   | Required | Description                              |
|-------------------|--------|----------|------------------------------------------|
| `file_name`        | string | No       | File name                                |
| `policy_number`    | string | No       | Policy number                            |
| `address`          | string | Yes      | Address                                   |
| `tenant`           | string | Yes      | Tenant name or ID                         |
| `payment_for`      | string | No       | Description of payment                    |
| `term_type`        | string | No       | Term type                                 |
| `lease_starts`     | string | Yes      | Start date (YYYY-MM-DD)                   |
| `lease_ends`       | string | Yes      | End date (YYYY-MM-DD)                     |
| `notes`            | string | No       | Additional notes                          |
| `amount`           | string | Yes      | Amount                                    |
| `landlord`         | string | Yes      | Landlord                                  |
| `landlord_signature`| string| No       | Landlord's signature                      |
| `date`             | string | Yes      | Creation date (YYYY-MM-DD)                |
| `property_id`      | string | Yes      | Associated property ID                    |
| `user_id`          | string | Yes      | Associated user ID                        |

#### Example Request

```json
{
  "file_name": "invoice1.pdf",
  "policy_number": "PN-2025-01",
  "address": "123 Main St",
  "tenant": "John Doe",
  "payment_for": "Insurance",
  "term_type": "Annual",
  "lease_starts": "2025-01-01",
  "lease_ends": "2025-12-31",
  "notes": "First invoice of year",
  "amount": "1500",
  "landlord": "Jane Smith",
  "landlord_signature": "Signed",
  "date": "2025-06-01",
  "property_id": "456",
  "user_id": "123"
}
```

#### Responses

- `200 OK` — Insert successful  
- `400` — Missing required fields  
- `500` — Database/server error

---

### PUT /tenantInvoice

Update an existing tenant invoice record by `id`.

#### Required in Body

- `id`: ID of the row to update  
- At least one updatable field

#### Updatable Fields

| Field               | Type   | Description                         |
|--------------------|--------|-------------------------------------|
| `file_name`         | string | Updated file name                   |
| `policy_number`     | string | Updated policy number               |
| `address`           | string | Updated address                     |
| `tenant`            | string | Updated tenant                      |
| `payment_for`       | string | Updated payment description         |
| `term_type`         | string | Updated term type                   |
| `lease_starts`      | string | Updated lease start date            |
| `lease_ends`        | string | Updated lease end date              |
| `notes`             | string | Updated notes                       |
| `amount`            | string | Updated amount                      |
| `landlord`          | string | Updated landlord                    |
| `landlord_signature`| string | Updated signature                   |
| `date`              | string | Updated invoice date                |
| `property_id`       | string | Updated property ID                 |
| `user_id`           | string | Updated user ID                     |

#### Example Request

```json
{
  "id": 1,
  "amount": "1600",
  "notes": "Revised amount"
}
```

#### Responses

- `200 OK` — Update successful  
- `400` — Missing or invalid `id`, or no updatable fields  
- `500` — Database/server error

---

### DELETE /tenantInvoice

Delete one or more invoice records.

#### Request Body

| Field | Type        | Required | Description                  |
|-------|-------------|----------|------------------------------|
| `id`  | int \| int[]| Yes      | ID or array of IDs to delete |

#### Example Request

```json
{ "id": 1 }
```

```json
{ "id": [2, 3, 4] }
```

#### Responses

- `200 OK` — Deletion successful  
- `400` — Missing or invalid `id`  
- `500` — Database/server error

## /tenantMaintenance/

Handles CRUD operations for tenant invoice records.

### Table Schema:

| Field               | Type         | Description                                 |
|--------------------|--------------|---------------------------------------------|
| id           | int(11)      | Auto-increment primary key                  |
| url           | varchar(255) | URL of the file                          |
| category       | varchar(255) | Category of Maintenance                            |
| cat_other             | varchar(255) | Any other category information        |
| contractor              | varchar(255) | Contractor Name                         |
| contractorOther         | varchar(255) | Any other contractor information          |
| message           | text  | Message contained in maintenance         |
| agentLandQuote        | 	varchar(255)	       | Any quotes involved           |
| cost          | 	varchar(255)	   | Cost of maintenance                |
| quoteOffer               | 	varchar(255)	        | Quote Offer contained                         |
| scheduleTechnician              | varchar(255) |                             |
| quoteApprove            | 	int(11) | Boolean for Approval of quote                      |
| quoteDecline  | 	int(11) | Boolean for Decline of quote         |
| completed                | 	int(11)         | Boolean for whether or not maintenance was completed   |
| technician           | int(11)      | Boolean for whether message was from technician               |
| agent           | int(11)      | Boolean for whether message was from agent                  |
| property_id         | int(11)      | Foreign key to a property                   |
| user_id             | int(11)      | Foreign key to a user                       |
| date_created             | varchar(50)      | Date created (YYYY-MM-DD HH:MM:SS am/pm)            |

---

### GET /tenantMaintenance/

Fetch tenant invoice records by specific query parameters.

#### Query Parameters

| Parameter       | Type   | Required | Description                             |
|-----------------|--------|----------|-----------------------------------------|
| `id`            | int    | No       | Fetch a specific record by ID           |
| `user_id`       | string | No       | Fetch records for a specific user       |
| `property_id`   | string | No       | Fetch records for a specific property   |
| `user_id` + `property_id` | string | No | Fetch records matching both fields      |

#### Rules

- You must provide either:
  - Exactly **1** of `id`, `user_id`, or `property_id`, **or**
  - Both `user_id` and `property_id`

#### Example Request

```http
GET /tenantMaintenance?user_id=123&property_id=456
```

#### Responses

- `400 Bad Request` — If invalid or missing parameters  
- `400 Data Not Found` — If no record matches

---

### POST /tenantMaintenance

Insert a new tenant invoice record.

#### Required Fields in Body (JSON)

| Field              | Type   | Required | Description                              |
|-------------------|--------|----------|------------------------------------------|
| url           | varchar(255) | No | URL of the file                          |
| category       | varchar(255) | No | Category of Maintenance                            |
| cat_other             | varchar(255) | No |  Any other category information        |
| contractor              | varchar(255) | No | Contractor Name                         |
| contractorOther         | varchar(255) | No | Any other contractor information          |
| message           | text  | No | Message contained in maintenance         |
| agentLandQuote        | 	varchar(255)	       | No | Any quotes involved           |
| cost          | 	varchar(255)	   | No | Cost of maintenance                |
| quoteOffer               | 	varchar(255)	        |No | Quote Offer contained                         |
| scheduleTechnician              | varchar(255) | No |                             |
| quoteApprove            | 	int(11) | No | Boolean for Approval of quote                      |
| quoteDecline  | 	int(11) | No | Boolean for Decline of quote         |
| completed                | 	int(11)         | No | Boolean for whether or not maintenance was completed   |
| technician           | int(11)      | No | Boolean for whether message was from technician               |
| agent           | int(11)      | No | Boolean for whether message was from agent                  |
| property_id         | int(11)      | Yes | Foreign key to a property                   |
| user_id             | int(11)      | Yes | Foreign key to a user                       |
| date_created             | varchar(50)      | Yes | Date created (YYYY-MM-DD HH:MM:SS am/pm)            |

Note: One of agent or technician must be set to 1.

#### Example Request

```json
{
  "message": "Please fix my stove",
  "technician": 1,
  "date_created": "2025-06-01",
  "property_id": "456",
  "user_id": "123"
}
```

#### Responses

- `200 OK` — Insert successful  
- `400` — Missing required fields  
- `500` — Database/server error

---

### PUT /tenantMaintenance

Update an existing tenant invoice record by `id`.

#### Required in Body

- `id`: ID of the row to update  
- At least one updatable field

#### Updatable Fields

| Field               | Type   | Description                         |
|--------------------|--------|-------------------------------------|
| url           | varchar(255) | URL of the file                          |
| category       | varchar(255) | Category of Maintenance                            |
| cat_other             | varchar(255) | Any other category information        |
| contractor              | varchar(255) | Contractor Name                         |
| contractorOther         | varchar(255) | Any other contractor information          |
| message           | text  | Message contained in maintenance         |
| agentLandQuote        | 	varchar(255)	       | Any quotes involved           |
| cost          | 	varchar(255)	   | Cost of maintenance                |
| quoteOffer               | 	varchar(255)	        | Quote Offer contained                         |
| scheduleTechnician              | varchar(255) |                             |
| quoteApprove            | 	int(11) | Boolean for Approval of quote                      |
| quoteDecline  | 	int(11) | Boolean for Decline of quote         |
| completed                | 	int(11)         | Boolean for whether or not maintenance was completed   |
| technician           | int(11)      | Boolean for whether message was from technician               |
| agent           | int(11)      | Boolean for whether message was from agent                  |
| property_id         | int(11)      | Foreign key to a property                   |
| user_id             | int(11)      | Foreign key to a user                       |
| date_created             | varchar(50)      | Date created (YYYY-MM-DD HH:MM:SS am/pm)            |

#### Example Request

```json
{
  "id": 1,
  "url": "new url",
}
```

#### Responses

- `200 OK` — Update successful  
- `400` — Missing or invalid `id`, or no updatable fields  
- `500` — Database/server error

---

### DELETE /tenantMaintenance

Delete one or more invoice records.

#### Request Body

| Field | Type        | Required | Description                  |
|-------|-------------|----------|------------------------------|
| `id`  | int \| int[]| Yes      | ID or array of IDs to delete |

#### Example Request

```json
{ "id": 1 }
```

```json
{ "id": [2, 3, 4] }
```

#### Responses

- `200 OK` — Deletion successful  
- `400` — Missing or invalid `id`  
- `500` — Database/server error

## /tenantPayment/

Handles CRUD operations for tenant payment records.

### Table Schema:

| Field        | Type      | Description                              |
|--------------|-----------|------------------------------------------|
| idPrimary    | int(11)   | Auto-increment primary key               |
| rent         | text      | Rent amount                              |
| status       | text      | Payment status                           |
| date         | text      | Date of payment                          |
| status_id    | int(11)   | Status identifier                        |
| term         | text      | Term of the payment                      |
| property_id  | int(11)   | Foreign key to a property                |
| user_id      | int(11)   | Foreign key to a user                    |

---

### GET /tenantPayment/

Fetch tenant payment records by specific query parameters.

#### Query Parameters

| Parameter       | Type   | Required | Description                             |
|-----------------|--------|----------|-----------------------------------------|
| `id`            | int    | No       | Fetch a specific record by ID           |
| `user_id`       | string | No       | Fetch records for a specific user       |
| `property_id`   | string | No       | Fetch records for a specific property   |
| `user_id` + `property_id` | string | No | Fetch records matching both fields      |

#### Rules

- You must provide either:
  - Exactly **1** of `id`, `user_id`, or `property_id`, **or**
  - Both `user_id` and `property_id`

#### Example Request

```http
GET /tenantPayment?user_id=123&property_id=456
```

#### Responses

- `400 Bad Request` — If invalid or missing parameters  
- `400 Data Not Found` — If no record matches

---

### POST /tenantPayment

Insert a new tenant payment record.

#### Required Fields in Body (JSON)

| Field         | Type   | Required | Description                    |
|--------------|--------|----------|--------------------------------|
| `rent`        | string | Yes      | Rent amount                    |
| `status`      | string | Yes      | Payment status                 |
| `date`        | string | Yes      | Date of payment                |
| `status_id`   | string | Yes      | Status identifier              |
| `term`        | string | Yes      | Term of the payment            |
| `property_id` | string | Yes      | Associated property ID         |
| `user_id`     | string | Yes      | Associated user ID             |

#### Example Request

```json
{
  "rent": "1800",
  "status": "Paid",
  "date": "2025-06-01",
  "status_id": "1",
  "term": "Monthly",
  "property_id": "456",
  "user_id": "123"
}
```

#### Responses

- `200 OK` — Insert successful  
- `400` — Missing required fields  
- `500` — Database/server error

---

### PUT /tenantPayment

Update an existing tenant payment record by `id`.

#### Required in Body

- `id`: ID of the row to update  
- At least one updatable field

#### Updatable Fields

| Field         | Type   | Description                    |
|--------------|--------|--------------------------------|
| `rent`        | string | Updated rent amount            |
| `status`      | string | Updated payment status         |
| `date`        | string | Updated payment date           |
| `status_id`   | string | Updated status ID              |
| `term`        | string | Updated term                   |
| `property_id` | string | Updated property ID            |
| `user_id`     | string | Updated user ID                |

#### Example Request

```json
{
  "id": 1,
  "rent": "1900",
  "status": "Late"
}
```

#### Responses

- `200 OK` — Update successful  
- `400` — Missing or invalid `id`, or no updatable fields  
- `500` — Database/server error

---

### DELETE /tenantPayment

Delete one or more payment records.

#### Request Body

| Field | Type        | Required | Description                  |
|-------|-------------|----------|------------------------------|
| `id`  | int \| int[]| Yes      | ID or array of IDs to delete |

#### Example Request

```json
{ "id": 1 }
```

```json
{ "id": [2, 3, 4] }
```

#### Responses

- `200 OK` — Deletion successful  
- `400` — Missing or invalid `id`  
- `500` — Database/server error
