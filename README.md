# Food-Delivery-App
## Features:
1. User Registeration & Authentication.
2. Restaurant & Menu Management.
3. Cart Management.
4. Order Management.
5. Payment Integration Management.
6. Customer Support Management.
7. Notification & Email Management
8. Dashboard & Reports
## Functions:
### 1. User Registeration & Authentication
     • Database Design 
        1. Customer
        2. Partner
        3. Delivery Captain
        4. Admin
     • API Endpoints
        1. Create Account /Sign Up
        2. Login
        3. Logout
        4. Forget Password
        5. Enable/Disable Account
        6. Third Party Authentication: Social Media, Google ...
        7. User Profile: Show, Edit.
### 2. Restaurant & Menu Management
     • Database Design 
        1. Resturant
        2. Menu
        3. Menu_Items
     • API Endpoints
        1. Add Restaurant         
        2. Update Restaurant      
        3. Delete Restaurant
        4. View Restaurants - Categories Tabs - Recommendations - Near You - Daily Offers- Top Rating ...      
        5. View Single Restaurant 
        6. Search Restaurant       
        7. Add Menu              
        8. Update Menu           
        9. Delete Menu          
        10. View Menu            
        11. Filter Menu / Item    
### 3. Cart Management
     •	Database Design 
        1. Cart 
        2. Cart_details
     •	API Endpoints
        1. Add to cart 
        2. Modify cart
            2.1 Add items
            2.2 Remove items
            2.3 Change quantity (+, -)
        3. Clear cart  
        4. Checkout
### 4. Order Management
     • Database Design 
        1. Order
        2. Order_Items
        3. Order_Status
     • API Endpoints
        1. Place Order     
        2. Cancel Order by customer/restaurant    
        3. Track Order
        4. View Order summary
        5. View Order details
        6. View Orders History
        7. Update Order Status
        8. Send Email confirmation
        9. Send order status notification
### 5. Payment Integration Management
     • Database Design 
        1. Transaction
        2. Payment Integration Type 
        3. Payment Integration Configuration
        4. Payment Status
        5. Customer Cart Info
        6. Partner Bank Account
        7. Auditing
     • API Endpoints
        1. Payment Integration with 3rd Party
        2. Select Payment method
        3. Customer Add Card
        4. Create Transaction
        5. View Payment Transaction
        6. Create Transaction Receipt
        7. send Email Notification 
### 6. Customer support Management
     • Database Design 
        1. Comments & Ratings
        2. Complains
     • API Endpoints
        1. Rasie a Complain
        2. Add Rate to restaurant
        3. Need Help       
 ### 7. Notification & Email Management
     • Database Design 
        1. Notifcations
        2. Emails
     • API Endpoints
        1. Send Notification
        2. Send Email
        
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
