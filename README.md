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
        3. Create Transaction
        4. View Payment Transaction
        5. Create Transaction Receipt
        6. send Email Notification 
### 6. Customer support Management
     • Database Design 
        1. Comments & Ratings
        2. Complains
     • API Endpoints
        1. Rasie a Complain
        2. Add Rate to restaurant
        3. Need Help     
        4. Customer Add Card
 ### 7. Notification & Email Management
     • Database Design 
        1. Notifcations
        2. Emails
     • API Endpoints
        1. Send Notification
        2. Send Email
        
## ERD
![System Architecture](docs/ERD-food_delivery_app.svg)

## Flowchart -Add To cart
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

### API Signature 
#### User Registeration
        - Sign up
                - signature /api/v1/user/signup
                - input [user_details{}]
                - output status code [201]
        - Sign in
                - signature /api/v1/user/signin
                - input [username, email,password]
                - output status code [200], Token
        - Signout
                - signature /api/v1/user/signout
                - input [customer_id]
                - output status code [200]
        - Forget password
                - signature /api/v1/user/forgetpass
                - input [email]
                - output status code [200]
        - Enable/disable account
                - signature /api/v1/user/account
                - input [customer_id, event_type]
                - output status code [200]
        - Show Profile
                - signature /api/v1/user/profile/:user_id
                - input [user_id]
                - output status code [200], user_details
        - Edit Profile
                - signature /api/v1/user/profile/:user_id
                - input [user_id,update_data]
                - output status code [201]
#### Cart management 
        - AddToCart
                - signature /api/v1/cart/add
                - input [customer_id,cart_items[]]
                - output status code [201]
        - ModifyCart
                - signature /api/v1/cart/:cart_id
                - input [cart_id, item_id, event_type]
                - output status code [201]
        - clearCart
                - signature /api/v1/cart/:cart_id
                - input [customer_id,cart_id]
                - output status code [200]
#### Order management 
        - placeOrder
                - signature /api/v1/order/add
                - input [customer_id,order_items[]]
                - output status code [201]
        - cancelOrder
                - signature /api/v1/order/cancel
                - input [customer_id,order_id]
                - output status code [200]
        - trackOrder
                - signature /api/v1/order/track
                - input [customer_id,order_id]
                - output order_status
        - viewOrder
                - signature /api/v1/order/:order_id
                - input [customer_id,order_id]
                - output order_details
        - viewOrders_History
                - signature /api/v1/order
                - input [customer_id]
                - output orders[]
         - Checkout
                - signature /api/v1/checkout
                - input [customer_id, payment_type, total_price]
                - output status code 201, transaction_details
#### Resturant & Menu management 
        - AddResturant
                - signature /api/v1/Resturant/add
                - input [partner_id,Resturant_details]
                - output status code [201]
        - updateResturant = put
                - signature /api/v1/resturant/:resturant_id
                - input [resturant_id,updated_data]
                - output status code [201]
        - deleteResturant
                - signature /api/v1/resturant/:resturant_id
                - input [resturant_id]
                - output status code 200
        - viewResturants
                - signature /api/v1/resturant
                - input []
                - output resturants[]
        - viewResturant
                - signature /api/v1/resturant/:resturant_id
                - input [resturant_id]
                - output resturant_details{}
        - addMenu
                - signature /api/v1/resturant/menu/add
                - input [resturant_id,menu_details]
                - output status code [201]
        - updateMenu
                - signature /api/v1/resturant/menu/:menu_id
                - input [menu_id, update_data]
                - output status code [201]
        - deleteMenu
                - signature /api/v1/resturant/menu/:menu_id
                - input [menu_id]
                - output status code [200]
        - viewMenu
                - signature /api/v1/resturant/menu/:menu_id
                - input [menu_id]
                - output menu_details
        - filterMenu
                - signature /api/v1/resturant/menu/filter
                - input [search_word]
                - output menu_details[]
  #### Payment management 
        - View Payment Transaction
                - signature /api/v1/payment/transaction
                - input [customer_id,transaction_id]
                - output status code [200], transaction_details
        - Add Rate
                - signature /api/v1/payment/receipt
                - input [customer_id, transaction_id]
                - output status code [200], tranastion_pdf
  #### Customer management 
        - Need Help
                - signature /api/v1/support/help
                - input [customer_id,need_type]
                - output status code [200]
        - Add Rate
                - signature /api/v1/support/rate
                - input [customer_id, resturant_id, rate, comment]
                - output status code [201]
         - Customer Add Card
                - signature /api/v1/support/addCart
                - input [customer_id, cart_details]
                - output status code [201]
