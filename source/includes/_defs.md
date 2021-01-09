# Object Definitions

Common object definitions

## Cart

```json
{
    "shop_id": "1a6c50ce-9006-4bda-bea4-2a6832f86684",
    "cart_id": "0a6c50ce-9006-4bda-bea4-2a6832f86684",
    "items": [
        // Array of CartItem
    ],
    "created": 1610181890,
    "updated": 1610181900,
    "expires": 1611391500, // updated + 14 days
    "items_amount": 0,
    "items_count": 0,
    "items_count_unique": 0,
    "shipping_amount": 0,
    "tax_amount": 0,
    "total_amount": 0
}
```

| Property           | Type   | Description                                   |
| ------------------ | ------ | --------------------------------------------- |
| shop_id            | String | The shop unique identifier                    |
| cart_id            | String | The cart unique identifier                    |
| items              | Array  | Items in the cart [CartItem](#cartitem)       |
| created            | Int    | The UNIX timestamp the cart was created       |
| updated            | Int    | The UNIX timestamp the cart was updated       |
| items_amount       | Int    | Sum of cart items                             |
| items_count        | Int    | Then number of total items in the cart        |
| items_count_unique | Int    | Then number of total unique items in the cart |
| shipping_amount    | Int    | The items shipping amount                     |
| tax_amount         | Int    | The items tax amount                          |
| total_amount       | Int    | The total amount of the cart                  |

## CartItem

```json
{
    "id": "SPARKRC900TEAM",
    "name": "Scott Spark RC900 Team Bike",
    "description": "The SCOTT Spark RC is perhaps the most successful full-suspension XC race bike of its time.",
    "price": 359998,
    "quantity": 1,
    "images": ["https://placehold.it/1600x1200"],
    "meta": {}
}
```

The cart item object reference. The cart item object is flexible, you can extend it using the **meta** property.

| Property    | Type     | Description                              |
| ----------- | -------- | ---------------------------------------- |
| id          | String\* | The cart item unique identifier          |
| name        | String\* | Item name                                |
| description | String\* | Item description                         |
| price       | Int\*    | Item price in cents (/100)               |
| quantity    | Int\*    | Item quantity                            |
| images      | Array    | Image URLs (must be publicly accessible) |
| meta        | Object   | Custom meta object                       |

<aside class="notice">
The fields marked with <strong>*</strong> are required
</aside>

## Customer

The customer object reference.

## Address

```json
// example of the address object
{
    "company": "",
    "name": "Marissa Doe", // required
    "line1": "132 Harvest Way", // required
    "line2": "",
    "city": "Crandall", // required
    "state": "TX",
    "postal_code": "75114", // required
    "country": "US" // required
}
```

| Field       | Type     | Description                                 |
| ----------- | -------- | ------------------------------------------- |
| company     | String   | Company name                                |
| name        | String\* | Recipient name                              |
| line1       | String\* | Address line 1                              |
| line2       | String   | Address line 2                              |
| city        | String\* | The address city                            |
| state       | String   | The address state/county/provice            |
| postal_code | String\* | The address post/zip code                   |
| country     | String\* | The address country (ISO 3166 Alpha-2 code) |

<aside class="notice">
The fields marked with <strong>*</strong> are required
</aside>
