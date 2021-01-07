# gumcart.js

```html
<script src="https://scripts.gumcart.com/latest.js"></script>
<script>
    window.GumCart && window.GumCart.init("shop/id");
</script>
```

gumcart.js is a small Javascript library that will help seamlessly integrate the shopping cart and checkout flow into a website.

Getting started is as easy:

1. Visit https://gumcart.com to get a shop ID.
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
    .then((item) => {
        // successfully added to cart
        console.log(item.name + " was added to cart");
    })
    .catch((err) => {
        // oops something bad happened
        console.log(err);
    });
```

Add a single item to the cart.

_Returns a Promise_

| Parameter | Description                                     |
| --------- | ----------------------------------------------- |
| id        | The unique identifier of the product _(string)_ |
| name      | Product name _(string)_                         |
| quantity  | Product quantity _(integer)_                    |
| price     | **REQUIRED**<br />Price _(float)_               |

See the list of the parameters on **The Cart Item Object**

## Update an item

```js
GumCart.updateItem(itemId, {
    quantity: 3,
})
    .then((item) => {
        // successfully updated
        console.log(item.name + " was updated");
    })
    .catch((err) => {
        // oops something bad happened
        console.log(err);
    });
```

Update properties of a single cart item by ID.

See the list of available properties on **The Cart Item Object**

_Returns a Promise_

## Remove an item

```js
GumCart.removeItem(itemId)
    .then((item) => {
        // successfully removed
        console.log(item.name + " was removed from the cart");
    })
    .catch((err) => {
        // oops something bad happened
        console.log(err);
    });
```

Remove a single item from the cart by ID.

_Returns a Promise_

## Get all items

```js
GumCart.getItems()
    .then((items) => {
        // successfully returned the array of items
        // loop through the array of items
        if (items.length) {
            items.forEach((item) => {
                console.log(item.name);
            });
        }
    })
    .catch((err) => {
        // oops something bad happened
        console.log(err);
    });
```

Get the list of items from the cart.

_Returns a Promise_

## Empty the cart

```js
GumCart.empty()
    .then(() => {
        // successfully emptied the cart
        console.log("The cart was emptied");
    })
    .catch((err) => {
        // oops something bad happened
        console.log(err);
    });
```

Removes all items from the cart.

_Returns a Promise_

## Update Customer Info

```js
GumCart.setCustomer({
    email: "john.doe@gumcart.com",
    name: "John Doe",
})
    .then((customer) => {
        // successfully updated customer info
        console.log("The customer info was updated.");
    })
    .catch((err) => {
        // oops something bad happened
        console.log(err);
    });
```

Update the checkout with customer information.

_Returns a Promise_

## Get Customer Info

```js
GumCart.getCustomer()
    .then((customer) => {
        // successfully received the customer info
        console.log("Customer name: " + customer.name);
    })
    .catch((err) => {
        // oops something bad happened
        console.log(err);
    });
```

Get the cart customer information.

_Returns a Promise_

## Update Shipping Info

```js
GumCart.setShipping({
    address: "132 Harvest Way",
    city: "Crandall",
    state: "TX",
    zip: "75114",
    country: "US",
    method: "flat",
})
    .then((shipping) => {
        // successfully updated shipping info
        console.log(shipping);
    })
    .catch((err) => {
        // oops something bad happened
        console.log(err);
    });
```

Update the cart with customer shipping information, address or shipping method.

_Returns TRUE/FALSE_

## Get Shipping Info

```js
GumCart.getShipping()
    .then((shipping) => {
        // successfully emptied the cart
        console.log("Shipping address:" + shipping.address);
    })
    .catch((err) => {
        // oops something bad happened
        console.log(err);
    });
```

Get the cart shipping information.

_Returns a Promise_

## Events

These events will fire anytime an action happen in the shopping cart or checkout flow. Use listeners to customise the experience.

```js
GumCart.on("ready", (data) => {
    // GumCart is loaded, do something here
});
```

```js
GumCart.on("totals.change", (data) => {
    // GumCart totals change, console log the amounts
    console.log("Shipping: $" + data.shipping_price);
    console.log("Tax: $" + data.tax_amount);
    console.log("Total amount: $" + data.total_amount);
});
```

| Event name      | Data     | Description                      |
| --------------- | -------- | -------------------------------- |
| ready           | -        | The cart is loaded & ready       |
| open            | -        | The shopping cart opened         |
| close           | -        | The shopping cart closed         |
| item.add        | item     | Item was added to cart           |
| item.update     | item     | The cart item was updated        |
| item.remove     | item     | Item was removed from cart       |
| totals.change   | totals   | Total amount of the cart changed |
| customer.change | customer | Customer data was updated        |
| shipping.change | shipping | Shipping info was updated        |
| billing.change  | billing  | Billing info was updated         |
| order.create    | order    | The order was created            |
