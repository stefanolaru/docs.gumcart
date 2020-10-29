# gumcart.js

```html
<script src="https://cdn.gumcart.com/cart.js"></script>
<script>
    window.GumCart && window.GumCart.init("shop/id");
</script>
```

gumcart.js is a small Javascript library that will help seamlessly integrate the shopping cart and checkout flow into a website.

Getting started is as easy:

1. Visit app.gumcart.com to get a shop ID.
2. Install gumcart.js via script tag.

```js
// opens the cart
GumCart.open();

// closes the cart
GumCart.close();
```

Now, let's use this code to open/close the shopping cart element.

Whoa! That's simple!

## The Cart Item

```json
{
    "id": "SPARKRC900TEAM",
    "name": "Scott Spark RC900 Team Bike",
    "price": 3599.98,
    "quantity": 1,
    "max_quantity": 1,
    "description": "The SCOTT Spark RC is perhaps the most successful full-suspension XC race bike of its time.",
    "sku": "280506",
    "image": "https://entry.clubfindersgolf.com/uploads/5f19dd565087d/bh111084a.jpg",
    "options": [
        { "name": "Frame Size", "value": "M" },
        { "name": "Color", "value": "Orange" }
    ],
    "addons": [
        { "name": "Oval Chainring", "price": 69 },
        { "name": "Syncros Bottle Cage (Left)", "price": 9.99 }
    ],
    "weight": 10900,
    "dimensions": {
        "length": 200,
        "width": 40,
        "height": 100
    }
}
```

The default cart item object reference. The cart item object is flexible, you can extend it with other properties.

| Property     | Description                        |
| ------------ | ---------------------------------- |
| id           | ID _(string)_                      |
| name         | Product name _(string)_            |
| price        | Price _(float)_                    |
| quantity     | Quantity _(integer)_               |
| max_quantity | Max available quantity _(integer)_ |
| description  | Product description _(string)_     |
| sku          | SKU _(string)_                     |
| image        | Image URL _(string)_               |
| options      | Product options _(array)_          |
| addons       | Product addons _(array)_           |
| weight       | Weight _(integer)_                 |
| dimensions   | Dimensions _(object)_              |

The price currency, weight & dimensions units are global settings, will pe set per shop basis.

## Add an item

```js
GumCart.addItem({
    id: "unique-product-id",
    name: "My nice Product",
    quantity: 1,
    price: 79.99,
})
    .then(() => {
        // This code runs once item was added
    })
    .catch((err) => {
        // This code runs if there were any errors
        console.log(err);
    });
```

Add a single item to the cart.

_Returns TRUE_

| Parameter | Description                                     |
| --------- | ----------------------------------------------- |
| id        | The unique identifier of the product _(string)_ |
| name      | Product name _(string)_                         |
| quantity  | Product quantity _(integer)_                    |
| price     | **REQUIRED**<br />Price _(float)_               |

See the list of the parameters on **The Cart Item Object**

## Update an item

```js
GumCart.updateItem("unique-product-id", {
    quantity: 3,
})
    .then(() => {
        // This code runs once item was added
    })
    .catch((err) => {
        // This code runs if there were any errors
        console.log(err);
    });
```

Update properties of a single cart item by ID.

See the list of available properties on **The Cart Item Object**

_Returns the updated cart item object_

## Remove an item

```js
GumCart.removeItem("unique-product-id")
    .then(() => {
        // This code runs once item was added
    })
    .catch((err) => {
        // This code runs if there were any errors
        console.log(err);
    });
```

Remove a single item from the cart by ID.

_Returns TRUE/FALSE_

## Get all items

```js
GumCart.getItems()
    .then((items) => {
        // we have the items here
        console.log(items);
    })
    .catch((err) => {
        // This code runs if there were any errors
        console.log(err);
    });
```

Get the list of items from the cart.

_Returns array of cart items_

## Empty the cart

```js
GumCart.empty();
```

Removes all items from the cart.

_Returns TRUE/FALSE_

## Update Customer Info

```js
GumCart.setCustomer({
    email: "john.doe@gumcart.com",
    name: "John Doe",
})
    .then(() => {
        // This code runs once customer data was set
    })
    .catch((err) => {
        // This code runs if there were any errors
        console.log(err);
    });
```

Update the cart with customer information.

_Returns TRUE/FALSE_

## Get Customer Data

```js
GumCart.getCustomer()
    .then((customer) => {
        // we have the customer data here
        console.log(customer);
    })
    .catch((err) => {
        // This code runs if there were any errors
        console.log(err);
    });
```

Get the cart customer information.

_Returns customer data object_

## Update Shipping Info

```js
GumCart.setShipping({
    address: {
        address: "132 Harvest Way",
        city: "Crandall",
        state: "TX",
        zip: "75114",
        country: "US",
    },
    method: "flat",
})
    .then(() => {
        // This code runs once customer data was set
    })
    .catch((err) => {
        // This code runs if there were any errors
        console.log(err);
    });
```

Update the cart with customer shipping information, address or shipping method.

_Returns TRUE/FALSE_

## Get Shipping Info

```js
GumCart.getShipping()
    .then((info) => {
        // we have the info here
        console.log(info);
        /*
        {
            address: {...},
            method: 'flat'
        }
        */
    })
    .catch((err) => {
        // This code runs if there were any errors
        console.log(err);
    });
```

Get the cart shipping information.

_Returns object_

## Set Shipping Value

```js
GumCart.setShippingValue(value)
    .then(() => {
        // this runs once value was set
    })
    .catch((err) => {
        // This code runs if there were any errors
        console.log(err);
    });
```

Sets the cart shipping value. This method allows you to create custom shipping cost calculation and override the cart one.

_Returns TRUE/FALSE_

## Events

```js
document.addEventListener("gumcart.ready", (e) => {
    // cart is loaded, do something here
});
```

| Event                | Description                                        |
| -------------------- | -------------------------------------------------- |
| gumcart.ready        | The shopping cart is loaded & ready                |
| gumcart.open         | The shopping cart opened                           |
| gumcart.close        | The shopping cart closed                           |
| gumcart.empty        | The shopping cart was emptied                      |
| gumcart.step         | The shopping cart switched from cart/checkout step |
| gumcart.item.added   | Item was added                                     |
| gumcart.item.removed | Item was removed                                   |
| gumcart.items.update | One of the cart items was updated                  |
| gumcart.value.update | The cart total amount was changed                  |
