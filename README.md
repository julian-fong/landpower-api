# landpower-api

Main Endpoint: https://www.landpower.ca/api/database

## /propertiesChat/

Columns

`id` : Retrieves a specific row id in the database
`message` : Text containing the message
`user_id` : Retrieves all messages from a specific `user_id`
`property_id`: Retrieves all messages for a specific `property_id`
`date_created` : Time and Date of the message

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
  "id": 1 // or [1, 2, 3] 
}
```
