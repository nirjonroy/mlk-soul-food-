<p align="center"><a href="https://mlksoulfood.com/" target="_blank"><img src="https://mlksoulfood.com/uploads/website-images/logo-2024-02-25-10-28-49-9781.png" width="400" alt="MLK Soul Food"></a></p>

# Laravel-Based E-Commerce Project

## Overview
This is a Laravel-based e-commerce platform that includes advanced cart functionality, payment methods, product variations, sides, and other dynamic options. The project supports both single and variable products with custom attributes and features like free and premium sides, credits, balance sheet integration, and Stripe payment.

## Features
### Product Management
- **Single and Variable Products:** Products can be of type 'single' or 'variable.'
- **Product Variations:** Variations have fields like `id`, `product_id`, `name`, and `product_price`. Examples include `Chicken Wings (5 Pieces)` and `Chicken Wings (10 Pieces).`
- **Options Management:** Products support additional options such as:
  - Flavour
  - Topping
  - Dip
  - Cheese
  - Veggies
  - Sauces
  - Protein

### Cart Functionality
- **Unique Cart Entries:** Each unique combination of product, variation, and options (e.g., sides, flavour, topping) creates a separate cart item.
- **Dynamic Pricing:**
  - Product variation price replaces the base price.
  - Additional options like sides, protein, and premium add-ons increase the final price dynamically.
- **Free Sides:** Free sides are limited to two selections per product.
- **Premium Sides:** Premium sides have no selection limit and their prices are added to the cart.
- **Dynamic Cart Storage:** The following details are stored in the cart:
  - Product Name (with Variation)
  - Quantity
  - Image
  - Price (variation + add-ons)
  - Selected Options (e.g., sides, protein, topping)

### Payment
- **Stripe Payment:** Redirects users to Stripe to complete payment and then navigates to a `thanks` page with `order_id` and `order_phone`.
- **Credit Payment:** Users can pay using credits if the balance covers the total order amount (including shipping fees).
  - Balance Sheet displays credit usage.
  - Validates if the available credit is sufficient.
- **Total Due Payment:** Users can view dues and make payments via Stripe or credit.

### Order Management
- **Order Status:** If `order_status == 6`, the total amount is updated in the user's `credit` field. The sold quantity (`sold_qty`) for each `product_id` is updated in the `products` table.
- **Dynamic Order Pages:**
  - Logged-in users see all orders via `url('order')`.
  - Non-logged-in users can view orders using their phone number (`order_phone`).

### Frontend Features
- **Product Gallery:** Supports multiple images displayed with horizontal scrolling. The gallery includes responsive layouts.
- **Image Slider:** Uses Owl Carousel for full-width sliders with autoplay, loop, and navigation.
- **Dynamic Options UI:**
  - Free sides display as radio buttons or checkboxes based on `sides_type`.
  - Premium sides are managed with checkboxes.

### Backend Management
- **Admin Functionality:**
  - Manage products, variations, options, and sides.
  - Update product information dynamically.
- **AJAX Integration:** Product options like sides are passed to the cart using AJAX.

## Key Tables and Models
1. **Product Table**
   - `product_type`: Defines 'single' or 'variable' product type.
2. **ProductVariation Table**
   - Handles variations with specific names and prices.
3. **Order Table**
   - Stores order details like `order_id`, `order_phone`, `order_status`, and total amounts.
4. **User Table**
   - Includes a `credit` field to track user credits.
5. **OrderProducts Table**
   - Tracks sold product quantities.
6. **FreeSide Model**
   - Manages free side options.

## Installation
1. **Clone the Repository:**
   ```bash
   git clone <repository-link>
   cd project-directory
   ```
2. **Install Dependencies:**
   ```bash
   composer install
   npm install && npm run dev
   ```
3. **Setup Database:**
   - Create a database and configure `.env` file:
     ```
     DB_DATABASE=your_database_name
     DB_USERNAME=your_username
     DB_PASSWORD=your_password
     ```
   - Run migrations:
     ```bash
     php artisan migrate --seed
     ```
4. **Run the Project:**
   ```bash
   php artisan serve
   ```
5. **Access Application:**
   Open `http://localhost:8000` in your browser.

## Technologies Used
- **Backend:** Laravel
- **Frontend:** Tailwind CSS, jQuery, Owl Carousel
- **Database:** MySQL
- **Payment Gateway:** Stripe
- **Additional Tools:** AJAX, JavaScript

## Usage
### Stripe Payment Flow
1. User selects products, variations, and options.
2. Proceeds to checkout.
3. Redirects to Stripe for payment.
4. On successful payment, navigates to a `thanks` page passing:
   - `order_id`
   - `order_phone`

### Credit Payment
1. User selects credit payment.
2. Validates if the balance covers the total order.
3. Deducts the credit from the user's account and proceeds to order completion.

### Free and Premium Sides
- Free sides allow a maximum of two options.
- Premium sides are unlimited and add prices dynamically.

## Future Improvements
- Add support for discounts and coupons.
- Enhance reporting for orders and credits.
- Introduce a user dashboard for better order tracking.
