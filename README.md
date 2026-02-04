<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FlavorDash | Gourmet Food Delivery</title>
    
    <!-- Font Awesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

    <style>
        /* --- CSS VARIABLES: Easily change colors here --- */
        :root {
            --primary-orange: #ff6600;
            --dark-grey: #333333;
            --light-grey: #f4f4f4;
            --white: #ffffff;
            --transition: all 0.3s ease;
        }

        /* --- GLOBAL STYLES --- */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }

        body {
            line-height: 1.6;
            color: var(--dark-grey);
            background-color: var(--white);
        }

        a { text-decoration: none; color: inherit; }
        ul { list-style: none; }
        button { cursor: pointer; border: none; outline: none; }

        /* --- NAVIGATION --- */
        header {
            background: var(--white);
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 5%;
            max-width: 1200px;
            margin: 0 auto;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary-orange);
        }

        .nav-links {
            display: flex;
            gap: 2rem;
        }

        .nav-links li a {
            font-weight: 500;
            transition: var(--transition);
        }

        .nav-links li a:hover {
            color: var(--primary-orange);
        }

        .cart-icon {
            position: relative;
            font-size: 1.2rem;
        }

        #cart-count {
            position: absolute;
            top: -10px;
            right: -10px;
            background: var(--primary-orange);
            color: white;
            font-size: 0.7rem;
            padding: 2px 6px;
            border-radius: 50%;
        }

        /* --- SECTION MANAGEMENT (SPA) --- */
        section {
            display: none; /* Hidden by default */
            padding: 5rem 5%;
            max-width: 1200px;
            margin: 0 auto;
            animation: fadeIn 0.5s ease;
        }

        section.active {
            display: block; /* Only active section shows */
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* --- 1. HOME / HERO SECTION --- */
        #home {
            text-align: center;
            padding-top: 8rem;
            background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), 
                        url('https://images.unsplash.com/photo-1504674900247-0877df9cc836?auto=format&fit=crop&w=1350&q=80');
            background-size: cover;
            background-position: center;
            color: white;
            min-height: 80vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            max-width: 100%;
        }

        .hero-content h1 { font-size: 3.5rem; margin-bottom: 1rem; }
        .hero-content p { font-size: 1.2rem; margin-bottom: 2rem; }
        
        .btn-order {
            background: var(--primary-orange);
            color: white;
            padding: 1rem 2.5rem;
            border-radius: 30px;
            font-size: 1.1rem;
            font-weight: 600;
            transition: var(--transition);
        }

        .btn-order:hover { background: #e65c00; transform: scale(1.05); }

        .featured-offers {
            margin-top: 4rem;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            color: var(--dark-grey);
        }

        .offer-card {
            background: var(--light-grey);
            padding: 20px;
            border-radius: 10px;
            border-left: 5px solid var(--primary-orange);
        }

        /* --- 2. MENU SECTION --- */
        .section-title {
            text-align: center;
            margin-bottom: 3rem;
            font-size: 2.5rem;
        }

        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
        }

        .food-card {
            background: var(--white);
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transition: var(--transition);
        }

        .food-card:hover { transform: translateY(-10px); }

        .food-card img {
            width: 100%;
            height: 200px;
            object-fit: cover;
        }

        .food-info { padding: 1.5rem; }
        .food-info h3 { margin-bottom: 0.5rem; }
        .price { color: var(--primary-orange); font-weight: 700; font-size: 1.2rem; }
        
        .stars { color: #ffcc00; margin: 0.5rem 0; }
        
        .add-to-cart-btn {
            width: 100%;
            background: var(--dark-grey);
            color: white;
            padding: 0.8rem;
            margin-top: 1rem;
            border-radius: 5px;
            transition: var(--transition);
        }

        .add-to-cart-btn:hover { background: var(--primary-orange); }

        /* --- 3. REVIEWS SECTION --- */
        .reviews-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin-bottom: 4rem;
        }

        .review-card {
            background: var(--light-grey);
            padding: 2rem;
            border-radius: 10px;
            position: relative;
        }

        .review-card i {
            color: var(--primary-orange);
            font-size: 2rem;
            opacity: 0.2;
            position: absolute;
            top: 10px; right: 10px;
        }

        .review-form {
            max-width: 600px;
            margin: 0 auto;
            background: var(--white);
            padding: 2rem;
            box-shadow: 0 0 20px rgba(0,0,0,0.05);
        }

        .form-group { margin-bottom: 1.5rem; }
        .form-group label { display: block; margin-bottom: 0.5rem; }
        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 5px;
        }

        /* --- 4. CONTACT SECTION --- */
        .contact-wrapper {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 4rem;
        }

        .contact-info h3 { margin-bottom: 1rem; color: var(--primary-orange); }
        .info-item { display: flex; align-items: center; gap: 1rem; margin-bottom: 1rem; }

        /* --- 5. CART SECTION --- */
        .cart-list { margin-bottom: 2rem; }
        .cart-item {
            display: flex;
            justify-content: space-between;
            padding: 1rem;
            border-bottom: 1px solid #eee;
        }
        .total-box {
            text-align: right;
            font-size: 1.5rem;
            font-weight: 700;
        }

        /* --- FOOTER --- */
        footer {
            background: var(--dark-grey);
            color: white;
            text-align: center;
            padding: 2rem;
            margin-top: 4rem;
        }

        /* --- MOBILE RESPONSIVENESS --- */
        @media (max-width: 768px) {
            .nav-links { display: none; } /* Simplified for demo: hidden on mobile */
            .hero-content h1 { font-size: 2.2rem; }
            .contact-wrapper { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

    <!-- NAVIGATION -->
    <header>
        <nav>
            <div class="logo">FlavorDash <i class="fas fa-utensils"></i></div>
            <ul class="nav-links">
                <li><a href="#" onclick="navigateTo('home')">Home</a></li>
                <li><a href="#" onclick="navigateTo('menu')">Menu</a></li>
                <li><a href="#" onclick="navigateTo('reviews')">Reviews</a></li>
                <li><a href="#" onclick="navigateTo('contact')">Contact</a></li>
            </ul>
            <div class="cart-icon" onclick="navigateTo('cart')" style="cursor: pointer;">
                <i class="fas fa-shopping-cart"></i>
                <span id="cart-count">0</span>
            </div>
        </nav>
    </header>

    <!-- 1. HOME SECTION -->
    <section id="home" class="active">
        <div class="hero-content">
            <h1>Delicious Food, Delivered Fast.</h1>
            <p>Experience the best local cuisines from the comfort of your home.</p>
            <button class="btn-order" onclick="navigateTo('menu')">Order Now</button>
        </div>

        <div class="featured-offers">
            <div class="offer-card">
                <h3>Buy 1 Get 1 Free</h3>
                <p>On all medium pizzas every Tuesday.</p>
            </div>
            <div class="offer-card">
                <h3>Free Delivery</h3>
                <p>For your first 3 orders above $20.</p>
            </div>
            <div class="offer-card">
                <h3>Weekend Special</h3>
                <p>20% Off on all family platters.</p>
            </div>
        </div>
    </section>

    <!-- 2. MENU / SHOP SECTION -->
    <section id="menu">
        <h2 class="section-title">Our Menu</h2>
        <div class="menu-grid" id="food-container">
            <!-- Food items will be generated by JS -->
        </div>
    </section>

    <!-- 3. REVIEWS SECTION -->
    <section id="reviews">
        <h2 class="section-title">Customer Reviews</h2>
        <div class="reviews-container">
            <div class="review-card">
                <i class="fas fa-quote-right"></i>
                <p>"The best burger I've had in years! Fast delivery and still hot."</p>
                <div class="stars"><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i></div>
                <strong>- John Doe</strong>
            </div>
            <div class="review-card">
                <i class="fas fa-quote-right"></i>
                <p>"Amazing sushi quality. The presentation was top-notch."</p>
                <div class="stars"><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="far fa-star"></i></div>
                <strong>- Sarah Smith</strong>
            </div>
            <div class="review-card">
                <i class="fas fa-quote-right"></i>
                <p>"Affordable and delicious. My go-to place for office lunch."</p>
                <div class="stars"><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star-half-alt"></i></div>
                <strong>- Mike Johnson</strong>
            </div>
        </div>

        <div class="review-form">
            <h3>Write a Review</h3>
            <form id="form-review">
                <div class="form-group">
                    <label>Name</label>
                    <input type="text" required placeholder="Your Name">
                </div>
                <div class="form-group">
                    <label>Rating</label>
                    <select required>
                        <option value="5">5 Stars</option>
                        <option value="4">4 Stars</option>
                        <option value="3">3 Stars</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Message</label>
                    <textarea rows="4" required placeholder="Share your experience..."></textarea>
                </div>
                <button type="submit" class="btn-order" style="width: 100%; border-radius: 5px;">Submit Review</button>
            </form>
        </div>
    </section>

    <!-- 4. CONTACT SECTION -->
    <section id="contact">
        <h2 class="section-title">Contact Us</h2>
        <div class="contact-wrapper">
            <div class="contact-info">
                <h3>Get In Touch</h3>
                <div class="info-item">
                    <i class="fas fa-map-marker-alt"></i>
                    <span>123 Foodie Street, Flavor Town, FT 5678</span>
                </div>
                <div class="info-item">
                    <i class="fas fa-phone"></i>
                    <span>+1 (555) 123-4567</span>
                </div>
                <div class="info-item">
                    <i class="fas fa-envelope"></i>
                    <span>support@flavordash.com</span>
                </div>
            </div>
            <form id="form-contact">
                <div class="form-group">
                    <label>Name</label>
                    <input type="text" required>
                </div>
                <div class="form-group">
                    <label>Email</label>
                    <input type="email" required>
                </div>
                <div class="form-group">
                    <label>Message</label>
                    <textarea rows="5" required></textarea>
                </div>
                <button type="submit" class="btn-order" style="width: 100%; border-radius: 5px;">Send Message</button>
            </form>
        </div>
    </section>

    <!-- 5. CART SECTION -->
    <section id="cart">
        <h2 class="section-title">Your Cart</h2>
        <div id="cart-items-list" class="cart-list">
            <!-- Cart items will appear here -->
            <p style="text-align:center;">Your cart is empty.</p>
        </div>
        <div class="total-box">
            Total: $<span id="cart-total-price">0.00</span>
        </div>
        <button class="btn-order" style="margin-top: 2rem; width: 100%;" onclick="checkoutAlert()">Proceed to Checkout</button>
    </section>

    <footer>
        <p>&copy; 2024 FlavorDash Food E-commerce. All rights reserved.</p>
    </footer>

    <script>
        /* --- 1. SPA NAVIGATION LOGIC --- */
        function navigateTo(sectionId) {
            // Remove active class from all sections
            const sections = document.querySelectorAll('section');
            sections.forEach(sec => sec.classList.remove('active'));
            
            // Add active class to targeted section
            document.getElementById(sectionId).classList.add('active');
            
            // Scroll to top
            window.scrollTo(0, 0);
        }

        /* --- 2. MENU DATA & GENERATION --- */
        const foodItems = [
            { id: 1, name: "Classic Cheeseburger", price: 12.99, rating: 4.8, img: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500" },
            { id: 2, name: "Pepperoni Pizza", price: 15.50, rating: 4.5, img: "https://images.unsplash.com/photo-1628840042765-356cda07504e?w=500" },
            { id: 3, name: "Fresh Sushi Roll", price: 18.00, rating: 4.9, img: "https://images.unsplash.com/photo-1579871494447-9811cf80d66c?w=500" },
            { id: 4, name: "Garden Salad", price: 9.99, rating: 4.2, img: "https://images.unsplash.com/photo-1512621776951-a57141f2eefd?w=500" },
            { id: 5, name: "Chicken Alfredo", price: 14.25, rating: 4.6, img: "https://images.unsplash.com/photo-1645112481338-358aa19683bc?w=500" },
            { id: 6, name: "Spicy Tacos", price: 11.00, rating: 4.7, img: "https://images.unsplash.com/photo-1565299585095-ad2524e18370?w=500" },
            { id: 7, name: "Chocolate Lava Cake", price: 7.50, rating: 5.0, img: "https://images.unsplash.com/photo-1624353335558-68ca05f0d451?w=500" },
            { id: 8, name: "Iced Caramel Latte", price: 5.25, rating: 4.4, img: "https://images.unsplash.com/photo-1572442388796-11668a67e53d?w=500" }
        ];

        function displayMenu() {
            const container = document.getElementById('food-container');
            container.innerHTML = foodItems.map(item => `
                <div class="food-card">
                    <img src="${item.img}" alt="${item.name}">
                    <div class="food-info">
                        <h3>${item.name}</h3>
                        <div class="stars">${generateStars(item.rating)} <span>(${item.rating})</span></div>
                        <p class="price">$${item.price.toFixed(2)}</p>
                        <button class="add-to-cart-btn" onclick="addToCart(${item.id})">Add to Cart</button>
                    </div>
                </div>
            `).join('');
        }

        function generateStars(rating) {
            let stars = '';
            for(let i=1; i<=5; i++) {
                stars += i <= rating ? '<i class="fas fa-star"></i>' : '<i class="far fa-star"></i>';
            }
            return stars;
        }

        /* --- 3. CART LOGIC --- */
        let cart = [];

        function addToCart(productId) {
            const product = foodItems.find(p => p.id === productId);
            cart.push(product);
            updateCartUI();
            
            // Feedback for user
            alert(`${product.name} added to cart!`);
        }

        function updateCartUI() {
            // Update counter
            document.getElementById('cart-count').innerText = cart.length;
            
            // Update Cart Page
            const cartList = document.getElementById('cart-items-list');
            const totalPriceElement = document.getElementById('cart-total-price');
            
            if(cart.length === 0) {
                cartList.innerHTML = '<p style="text-align:center;">Your cart is empty.</p>';
                totalPriceElement.innerText = "0.00";
                return;
            }

            let total = 0;
            cartList.innerHTML = cart.map((item, index) => {
                total += item.price;
                return `
                    <div class="cart-item">
                        <span>${item.name}</span>
                        <span>$${item.price.toFixed(2)}</span>
                    </div>
                `;
            }).join('');

            totalPriceElement.innerText = total.toFixed(2);
        }

        function checkoutAlert() {
            if(cart.length === 0) {
                alert("Your cart is empty!");
            } else {
                alert("Order placed successfully! Thank you for choosing FlavorDash.");
                cart = [];
                updateCartUI();
                navigateTo('home');
            }
        }

        /* --- 4. FORM SUBMISSIONS --- */
        document.getElementById('form-review').addEventListener('submit', function(e) {
            e.preventDefault();
            alert("Thank you for your review! It will be posted after moderation.");
            this.reset();
        });

        document.getElementById('form-contact').addEventListener('submit', function(e) {
            e.preventDefault();
            alert("Message Sent! Our team will contact you shortly.");
            this.reset();
        });

        // Initialize Menu
        displayMenu();
    </script>
</body>
</html>
