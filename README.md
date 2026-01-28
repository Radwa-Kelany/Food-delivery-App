# Food-Delivery-App
## Features and Functions:
### 1. Cart Management Feature 
     •	Database Design 
        1.	Cart 
        2.	Cart_details
     •	API Endpoints
        1.	Add to cart 
        2.	Modify cart
            2.1 Add items
            2.2 Remove items
            2.3 Change quantity (+, -)
        3.	Clear cart  
## EDR
![System Architecture](docs/add_to_cart-EDR.svg)
## Flowchart 
![System Architecture](docs/add_to_cart-flowchart.svg)
 ## Sequence Diagram - Add to cart
![System Architecture](docs/add_to_cart-sequence_diagram.svg)

 ## Sequence Diagram - Modify cart
 ![System Architecture](docs/modify_cart-sequence_diagram.svg)

## PseudoCode
### 1. Add to cart 
```javascript
// Add To Cart API
function addToCart(customer_id, cart_items) {
  // Check if customer has Cart in Cache
  let cart_id;
  const cartId = getCartId(customer_id);
  // Yes
  if (cartId) {
    cart_id = cartId;
    // No ----> create new cart and get cart_id
  } else {
    createNewCart(customer_id);
    const newCartId = getCartId(customer_id);
    cart_id = newCartId;
  }
  AddCartItem(cart_id, cart_items);
}
```
### 2. View Cart 
```javascript
// View Cart API
function viewCart(customer_id) {
  let cart_items;
  try {
    const cart_id = getCartId(customer_id);
    const cartItems = getCartItems(cart_id);
    cart_items = cartItems;
  } catch (error) {
    return error;
  }
  return cart_items;
}
```

### 3. Modify Cart
#### 3.1 Remove Item
```javascript
// 1- Remove Item
function removeCartItem(cart_id, item_id) {
  try {
    const Item = getItemDetails(cart_id, item_id);
    if (Item) {
      deleteItemDetails(cart_id, item_id);
    }
  } catch (error) {
    return error;
  }
}
```

#### 3.2 Update quantity
```javascript
//     A- increase quantity
function IncrementQuantity(cart_id, item_id) {
  // Check if stock is available in DB server
  // get current quantity from Cache
  const { quantity } = getItemDetails(cart_id, item_id);
  // get stock quantity from DB server
  const { stock_quantity } = getItem(item_id);

  if (stock_quantity > quantity) {
    increaseQuantity(cart_id, item_id);
  } else {
    return error;
  }
}

//  B- decrease quantity
decrementQuantity(cart_id, item_id);
```
