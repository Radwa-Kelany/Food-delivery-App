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
