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
