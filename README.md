# landpower-api

### GET /properties/{id}

Retrieve a property listing by its ID.

#### Parameters
| Name | Type   | In   | Required | Description      |
|------|--------|------|----------|------------------|
| id   | string | path | yes      | Property ID      |

#### Response
- `200 OK`: JSON property object
- `404 Not Found`: if ID doesn't exist

```json
{
  "id": "123",
  "name": "Downtown Condo",
  "price": 450000,
  "available": true
}
