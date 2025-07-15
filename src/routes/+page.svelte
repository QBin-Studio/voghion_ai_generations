<script lang="ts">
  let searchQuery = '';
  let cartCount = 0;
  let isMenuOpen = false;
  let currentSlide = 0;
  let categorySlidePosition = 0;
  
  const categories = [
    'Local Warehouse',
    'Women\'s Clothing',
    'Men\'s Clothing', 
    'Apparel Accessories',
    'Shoes',
    'Luggage & Bags',
    'Denim',
    'E-scooters',
    'E-bikes',
    'Ramadan Picks'
  ];

  const heroSlides = [
    {
      id: 1,
      title: "Nature's Calling",
      subtitle: "Your camping adventure starts here >>",
      image: "https://images.unsplash.com/photo-1504280390367-361c6d9f38f4?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2070&q=80",
      cta: "Shop Now"
    },
    {
      id: 2,
      title: "Summer Collection",
      subtitle: "Beat the heat with our latest arrivals",
      image: "https://images.unsplash.com/photo-1441986300917-64674bd600d8?ixlib=rb-4.0.3&auto=format&fit=crop&w=2070&q=80",
      cta: "Explore"
    },
    {
      id: 3,
      title: "Flash Sale",
      subtitle: "Up to 70% off on selected items",
      image: "https://images.unsplash.com/photo-1472851294608-062f824d29cc?ixlib=rb-4.0.3&auto=format&fit=crop&w=2070&q=80",
      cta: "Shop Sale"
    }
  ];

  const movingCategories = [
    { name: 'Popular Categories', icon: '🔥', image: 'https://images.unsplash.com/photo-1441986300917-64674bd600d8?w=200&h=200&fit=crop' },
    { name: 'Shoes', icon: '👟', image: 'https://images.unsplash.com/photo-1549298916-b41d501d3772?w=200&h=200&fit=crop' },
    { name: 'Men\'s Clothing', icon: '👔', image: 'https://images.unsplash.com/photo-1506629905607-45bd62810a97?w=200&h=200&fit=crop' },
    { name: 'Luggage & Bags', icon: '🎒', image: 'https://images.unsplash.com/photo-1553062407-98eeb64c6a62?w=200&h=200&fit=crop' },
    { name: 'Apparel Accessories', icon: '👑', image: 'https://images.unsplash.com/photo-1506629905607-45bd62810a97?w=200&h=200&fit=crop' },
    { name: 'Women\'s Clothing', icon: '👗', image: 'https://images.unsplash.com/photo-1485518882345-15568b007407?w=200&h=200&fit=crop' },
    { name: 'Watches', icon: '⌚', image: 'https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=200&h=200&fit=crop' },
    { name: 'Sports & Outdoor', icon: '⚽', image: 'https://images.unsplash.com/photo-1571019613454-1cb2f99b2d8b?w=200&h=200&fit=crop' }
  ];

  const flashDeals = [
    {
      id: 1,
      name: 'All Metal Vintage T9 Machine Women\'s Hair Clipper',
      price: '$18.77',
      originalPrice: '$25.65',
      discount: '-27%',
      image: 'https://images.unsplash.com/photo-1522337360788-8b13dee7a37e?w=300&h=300&fit=crop',
      sold: '4 sold',
      badge: 'Lightning deal'
    },
    {
      id: 2,
      name: 'Outdoor 60L Large Capacity Backpack',
      price: '$26.95',
      originalPrice: '$60.14',
      discount: '-55%',
      image: 'https://images.unsplash.com/photo-1553062407-98eeb64c6a62?w=300&h=300&fit=crop',
      sold: '28 sold',
      badge: 'Lightning deal'
    },
    {
      id: 3,
      name: '12V Cleaning Go Kart For Kids',
      price: '$141.61',
      originalPrice: '$179.26',
      discount: '-21%',
      image: 'https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=300&h=300&fit=crop',
      sold: 'Limited time offer',
      badge: 'Lightning deal'
    },
    {
      id: 4,
      name: '6V Kids Electric ATV 4 Wheels Ride-On Toy',
      price: '$167.22',
      originalPrice: '$257.26',
      discount: '-35%',
      image: 'https://images.unsplash.com/photo-1558618047-3c8c76ca7d13?w=300&h=300&fit=crop',
      sold: 'Lightning deal',
      badge: 'Lightning deal'
    },
    {
      id: 5,
      name: 'Toddler Swing Set with Safety Harness',
      price: '$151.65',
      originalPrice: '$194.41',
      discount: '-22%',
      image: 'https://images.unsplash.com/photo-1544551763-46a013bb70d5?w=300&h=300&fit=crop',
      sold: 'Lightning deal',
      badge: 'Lightning deal'
    },
    {
      id: 6,
      name: 'Outsunny Kids Seesaw Swivel Teeter Totter',
      price: '$136.72',
      originalPrice: '$189.89',
      discount: '-28%',
      image: 'https://images.unsplash.com/photo-1551698618-1dfe5d97d256?w=300&h=300&fit=crop',
      sold: 'Limited time offer',
      badge: 'Lightning deal'
    }
  ];

  const newArrivals = [
    {
      id: 1,
      name: 'Waterproof Makeup Case',
      price: '$44.21',
      originalPrice: '$72.48',
      image: 'https://images.unsplash.com/photo-1596462502278-27bfdc403348?w=300&h=300&fit=crop'
    },
    {
      id: 2,
      name: 'High-end Full Drill Waterproof Calendar Men\'s Watch',
      price: '$57.93',
      originalPrice: '$91.96',
      image: 'https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=300&h=300&fit=crop'
    },
    {
      id: 3,
      name: 'Mini Handheld Fan USB Desk Fan',
      price: '$16.17',
      originalPrice: '$26.07',
      image: 'https://images.unsplash.com/photo-1581833971358-2c8b550f87b3?w=300&h=300&fit=crop'
    },
    {
      id: 4,
      name: 'Lenovo Wireless Waterproof Neckband Earphones',
      price: '$22.27',
      originalPrice: '$29.69',
      image: 'https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=300&h=300&fit=crop'
    }
  ];

  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }

  function addToCart() {
    cartCount++;
  }

  function nextSlide() {
    currentSlide = (currentSlide + 1) % heroSlides.length;
  }

  function prevSlide() {
    currentSlide = currentSlide === 0 ? heroSlides.length - 1 : currentSlide - 1;
  }

  function goToSlide(index: number) {
    currentSlide = index;
  }

  setInterval(() => {
    categorySlidePosition = (categorySlidePosition + 1) % movingCategories.length;
  }, 3000);

  setInterval(() => {
    nextSlide();
  }, 5000);
</script>

<svelte:head>
  <title>Voghion US | Online Shopping for Fashion & Lifestyle</title>
  <meta name="description" content="Shop the latest fashion trends, accessories, and lifestyle products at Voghion. Free shipping & Exclusive coupons." />
</svelte:head>

<div class="app">
  <header class="header">
    <div class="header-top">
      <div class="container">
        <div class="header-info">
          <div class="left-info">
            <span>Hi, <a href="/signin">Sign in</a> / <a href="/register">Register</a></span>
            <span>Free shipping & Exclusive coupons</span>
            <span>Delivery guarantee | Refund for any issue</span>
          </div>
          <div class="right-info">
            <a href="/ip-protection">IP Protection Portal</a>
            <a href="/support">Support & Help</a>
          </div>
        </div>
      </div>
    </div>

    <div class="header-main">
      <div class="container">
        <div class="header-content">
          <div class="logo">
            <a href="/">
              <div class="logo-icon">V</div>
              <span>oghion</span>
            </a>
          </div>

          <div class="shop-category">
            <button class="category-btn">
              Shop by category
              <svg width="12" height="12" viewBox="0 0 24 24" fill="none">
                <path d="M6 9L12 15L18 9" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
              </svg>
            </button>
          </div>

          <div class="search-bar">
            <input 
              type="text" 
              placeholder="Search"
              bind:value={searchQuery}
            />
            <button type="submit" class="search-btn">Search</button>
          </div>

          <div class="header-actions">
            <div class="language-currency">
              <img src="https://flagcdn.com/w20/us.png" alt="US" />
              <span>EN<br/>USD</span>
            </div>
            
            <a href="/cart" class="cart-link">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                <path d="M3 3H5L5.4 5M7 13H17L21 5H5.4M7 13L5.4 5M7 13L4.7 15.3C4.3 15.7 4.6 16.5 5.1 16.5H17M17 13V16.5M9 19.5C9.8 19.5 10.5 20.2 10.5 21S9.8 22.5 9 22.5 7.5 21.8 7.5 21 8.2 19.5 9 19.5ZM20 19.5C20.8 19.5 21.5 20.2 21.5 21S20.8 22.5 20 22.5 18.5 21.8 18.5 21 19.2 19.5 20 19.5Z" stroke="currentColor" stroke-width="2"/>
              </svg>
              <span class="cart-count">{cartCount}</span>
              <span>Cart</span>
            </a>

            <div class="support-chat">
              <div class="chat-icon">🐕</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <nav class="navigation">
      <div class="container">
        <ul class="nav-menu">
          {#each categories as category}
            <li><a href="/category/{category.toLowerCase().replace(/\s+/g, '-')}">{category}</a></li>
          {/each}
        </ul>
      </div>
    </nav>
  </header>

  <main class="main">
    <section class="hero-carousel">
      <div class="carousel-container">
        <div class="carousel-slides" style="transform: translateX(-{currentSlide * 100}%)">
          {#each heroSlides as slide}
            <div class="slide">
              <img src={slide.image} alt={slide.title} />
              <div class="slide-content">
                <h1>{slide.title}</h1>
                <p>{slide.subtitle}</p>
                <a href="/camping" class="cta-link">{slide.cta}</a>
              </div>
            </div>
          {/each}
        </div>
        
        <button class="carousel-btn prev" on:click={prevSlide}>❮</button>
        <button class="carousel-btn next" on:click={nextSlide}>❯</button>
        
        <div class="carousel-dots">
          {#each heroSlides as _, index}
            <button 
              class="dot" 
              class:active={index === currentSlide}
              on:click={() => goToSlide(index)}
            ></button>
          {/each}
        </div>
      </div>
    </section>

    <section class="commitment-section">
      <div class="container">
        <div class="commitment-items">
          <div class="commitment-item">
            <span class="icon">🛡️</span>
            <span>Voghion's Commitment</span>
          </div>
          <div class="commitment-item">
            <span class="icon">🔒</span>
            <span>Secure privacy</span>
          </div>
          <div class="commitment-item">
            <span class="icon">💳</span>
            <span>Safe Payments</span>
          </div>
          <div class="commitment-item">
            <span class="icon">🚚</span>
            <span>Delivery guarantee</span>
          </div>
          <button class="view-more">View →</button>
        </div>
        
        <div class="security-reminder">
          <span class="warning-icon">⚠️</span>
          <span>Security reminder: Please be wary of scam messages and links. Voghion won't ask for extra fees via SMS or email.</span>
          <button class="view-link">View →</button>
        </div>
      </div>
    </section>

    <section class="summer-categories">
      <div class="container">
        <div class="section-header">
          <div class="summer-title">
            <span class="summer-icon">🏖️</span>
            <span class="summer-text">Summer</span>
            <span class="sale-text">Sale</span>
            <span class="palm-icon">🌴</span>
          </div>
          <h2>CATEGORIES</h2>
        </div>
        
        <div class="moving-categories">
          <div class="categories-track" style="transform: translateX(-{categorySlidePosition * 200}px)">
            {#each [...movingCategories, ...movingCategories] as category}
              <div class="category-item">
                <img src={category.image} alt={category.name} />
                <span>{category.name}</span>
              </div>
            {/each}
          </div>
        </div>
      </div>
    </section>

    <section class="flash-deals">
      <div class="container">
        <div class="section-header-flash">
          <h2>⚡ Flash Deals</h2>
          <span>Don't Miss Out - Incredible Deals Await</span>
          <button class="view-more">View More →</button>
        </div>
        
        <div class="deals-grid">
          {#each flashDeals as product}
            <div class="deal-card">
              <div class="product-image">
                <img src={product.image} alt={product.name} />
                <div class="discount-badge">{product.discount}</div>
                <div class="lightning-badge">{product.badge}</div>
              </div>
              <div class="product-info">
                <h3>{product.name}</h3>
                <div class="price">
                  <span class="current-price">{product.price}</span>
                  <span class="original-price">{product.originalPrice}</span>
                </div>
                <div class="sold-info">{product.sold}</div>
              </div>
            </div>
          {/each}
        </div>
      </div>
    </section>

    <section class="new-arrivals-section">
      <div class="container">
        <div class="two-column-layout">
          <div class="column">
            <div class="section-header-simple">
              <h2>New Arrivals</h2>
              <p>Ships from Local Warehouse</p>
              <button class="view-more">View More →</button>
            </div>
            <div class="products-row">
              {#each newArrivals.slice(0, 2) as product}
                <div class="new-arrival-card">
                  <img src={product.image} alt={product.name} />
                  <div class="product-details">
                    <h4>{product.name}</h4>
                    <div class="price">
                      <span class="current">{product.price}</span>
                      <span class="original">{product.originalPrice}</span>
                    </div>
                  </div>
                </div>
              {/each}
            </div>
          </div>
          
          <div class="column">
            <div class="section-header-simple">
              <h2>Clearance Sale</h2>
              <p>Unbeatable Discounts on Last Chance Items</p>
              <button class="view-more">View More →</button>
            </div>
            <div class="products-row">
              {#each newArrivals.slice(2, 4) as product}
                <div class="new-arrival-card">
                  <img src={product.image} alt={product.name} />
                  <div class="product-details">
                    <h4>{product.name}</h4>
                    <div class="price">
                      <span class="current">{product.price}</span>
                      <span class="original">{product.originalPrice}</span>
                    </div>
                  </div>
                </div>
              {/each}
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>

  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-section">
          <h3>Company info</h3>
          <ul>
            <li><a href="/about">About Voghion</a></li>
            <li><a href="/affiliate">Voghion Affiliate Program</a></li>
            <li><a href="/blog">Voghion Blog</a></li>
            <li><a href="/imprint">Imprint</a></li>
          </ul>
        </div>

        <div class="footer-section">
          <h3>Customer Service</h3>
          <ul>
            <li><a href="/contact">Contact us</a></li>
            <li><a href="/shipping">Shipping Policy</a></li>
            <li><a href="/returns">Return Policy</a></li>
            <li><a href="/refund">Refund Policy</a></li>
            <li><a href="/ip-policy">Intellectual Property Policy</a></li>
          </ul>
        </div>

        <div class="footer-section">
          <h3>Help & Support</h3>
          <ul>
            <li><a href="/coupon">Voghion Coupon</a></li>
            <li><a href="/support">Support Center & FAQ</a></li>
            <li><a href="/payment">Payment Method</a></li>
            <li><a href="/student">Student Discount</a></li>
          </ul>
        </div>

        <div class="footer-section">
          <h3>Connect with Voghion</h3>
          <div class="social-links">
            <a href="#" aria-label="Instagram">📷</a>
            <a href="#" aria-label="TikTok">🎵</a>
            <a href="#" aria-label="Facebook">📘</a>
            <a href="#" aria-label="Pinterest">📌</a>
            <a href="#" aria-label="Discord">💬</a>
          </div>
        </div>
      </div>

      <div class="payment-section">
        <h3>WE ACCEPT</h3>
        <div class="payment-methods">
          <img src="https://via.placeholder.com/40x25/0070BA/FFFFFF?text=PP" alt="PayPal" />
          <img src="https://via.placeholder.com/40x25/1A1F71/FFFFFF?text=VISA" alt="Visa" />
          <img src="https://via.placeholder.com/40x25/EB001B/FFFFFF?text=MC" alt="Mastercard" />
          <img src="https://via.placeholder.com/40x25/006FCF/FFFFFF?text=AMEX" alt="American Express" />
          <img src="https://via.placeholder.com/40x25/00A1F1/FFFFFF?text=JCB" alt="JCB" />
          <img src="https://via.placeholder.com/40x25/00A3E0/FFFFFF?text=UP" alt="UnionPay" />
        </div>
      </div>

      <div class="trustpilot-section">
        <div class="trustpilot-widget">
          <span>Our customers say Great ⭐⭐⭐⭐⭐ 4.3 out of 5 based on 6,260 reviews</span>
          <img src="https://via.placeholder.com/100x30/00B67A/FFFFFF?text=Trustpilot" alt="Trustpilot" />
        </div>
      </div>

      <div class="footer-bottom">
        <p>@ 2025 Voghion</p>
        <div class="legal-links">
          <a href="/privacy">Privacy & cookie policy</a>
          <a href="/terms">Terms & Conditions</a>
        </div>
      </div>
    </div>
  </footer>
</div>

<style>
  :global(*) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :global(body) {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    line-height: 1.4;
    color: #333;
  }

  .app {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }

  .container {
    max-width: 1400px;
    margin: 0 auto;
    padding: 0 20px;
  }

  .header-top {
    background: #f8f9fa;
    padding: 6px 0;
    font-size: 12px;
    border-bottom: 1px solid #e9ecef;
  }

  .header-info {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .left-info {
    display: flex;
    gap: 25px;
  }

  .left-info span, .right-info {
    color: #666;
  }

  .left-info a, .right-info a {
    color: #007bff;
    text-decoration: none;
  }

  .right-info {
    display: flex;
    gap: 20px;
  }

  .header-main {
    background: white;
    padding: 12px 0;
    border-bottom: 1px solid #e9ecef;
  }

  .header-content {
    display: flex;
    align-items: center;
    gap: 20px;
  }

  .logo {
    flex-shrink: 0;
  }

  .logo a {
    display: flex;
    align-items: center;
    gap: 2px;
    text-decoration: none;
    color: #333;
    font-size: 24px;
    font-weight: bold;
  }

  .logo-icon {
    background: #ff4757;
    color: white;
    width: 32px;
    height: 32px;
    border-radius: 6px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 18px;
    font-weight: bold;
  }

  .shop-category {
    flex-shrink: 0;
  }

  .category-btn {
    background: none;
    border: 1px solid #ddd;
    padding: 10px 15px;
    border-radius: 6px;
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 14px;
    color: #666;
  }

  .search-bar {
    flex: 1;
    display: flex;
    max-width: 600px;
  }

  .search-bar input {
    flex: 1;
    padding: 12px 16px;
    border: 2px solid #e9ecef;
    border-radius: 25px 0 0 25px;
    outline: none;
    font-size: 14px;
  }

  .search-btn {
    padding: 12px 24px;
    background: #333;
    color: white;
    border: 2px solid #333;
    border-radius: 0 25px 25px 0;
    cursor: pointer;
    font-size: 14px;
    font-weight: 500;
  }

  .header-actions {
    display: flex;
    align-items: center;
    gap: 20px;
    flex-shrink: 0;
  }

  .language-currency {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 12px;
    font-weight: 500;
  }

  .language-currency img {
    width: 20px;
    height: auto;
  }

  .cart-link {
    display: flex;
    align-items: center;
    gap: 8px;
    text-decoration: none;
    color: #333;
    position: relative;
  }

  .cart-count {
    background: #ff4757;
    color: white;
    border-radius: 50%;
    width: 20px;
    height: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
    position: absolute;
    top: -5px;
    left: 15px;
  }

  .support-chat {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: #ffd32a;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
  }

  .chat-icon {
    font-size: 20px;
  }

  .navigation {
    background: white;
    border-bottom: 1px solid #e9ecef;
    padding: 0;
  }

  .nav-menu {
    display: flex;
    list-style: none;
    gap: 0;
    overflow-x: auto;
  }

  .nav-menu li a {
    display: block;
    padding: 15px 20px;
    color: #333;
    text-decoration: none;
    font-size: 14px;
    white-space: nowrap;
    transition: background-color 0.2s;
  }

  .nav-menu li a:hover {
    background: #f8f9fa;
  }

  .main {
    flex: 1;
  }

  .hero-carousel {
    position: relative;
    height: 400px;
    overflow: hidden;
  }

  .carousel-container {
    position: relative;
    width: 100%;
    height: 100%;
  }

  .carousel-slides {
    display: flex;
    width: 300%;
    height: 100%;
    transition: transform 0.5s ease;
  }

  .slide {
    flex: 1;
    position: relative;
    height: 100%;
  }

  .slide img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .slide-content {
    position: absolute;
    left: 60px;
    top: 50%;
    transform: translateY(-50%);
    color: white;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
  }

  .slide-content h1 {
    font-size: 48px;
    margin-bottom: 12px;
    font-weight: bold;
    font-style: italic;
  }

  .slide-content p {
    font-size: 18px;
    margin-bottom: 24px;
  }

  .cta-link {
    color: white;
    text-decoration: underline;
    font-size: 16px;
  }

  .carousel-btn {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: rgba(0,0,0,0.5);
    color: white;
    border: none;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    cursor: pointer;
    font-size: 18px;
    z-index: 10;
  }

  .carousel-btn.prev {
    left: 20px;
  }

  .carousel-btn.next {
    right: 20px;
  }

  .carousel-dots {
    position: absolute;
    bottom: 20px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    gap: 8px;
  }

  .dot {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    border: none;
    background: rgba(255,255,255,0.5);
    cursor: pointer;
  }

  .dot.active {
    background: white;
  }

  .commitment-section {
    background: #fff8e1;
    padding: 15px 0;
  }

  .commitment-items {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 10px;
  }

  .commitment-item {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 14px;
  }

  .security-reminder {
    display: flex;
    align-items: center;
    gap: 10px;
    font-size: 13px;
    color: #666;
  }

  .view-more, .view-link {
    background: none;
    border: none;
    color: #007bff;
    cursor: pointer;
    font-size: 14px;
  }

  .summer-categories {
    padding: 40px 0;
    background: white;
  }

  .section-header {
    text-align: center;
    margin-bottom: 30px;
  }

  .summer-title {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    margin-bottom: 10px;
    font-size: 24px;
  }

  .summer-text {
    color: #4fc3f7;
    font-weight: bold;
  }

  .sale-text {
    color: #ffd54f;
    font-weight: bold;
  }

  .section-header h2 {
    font-size: 32px;
    font-weight: bold;
    color: #333;
    letter-spacing: 2px;
  }

  .moving-categories {
    overflow: hidden;
    width: 100%;
  }

  .categories-track {
    display: flex;
    gap: 30px;
    transition: transform 0.5s ease;
    animation: slide 20s infinite linear;
  }

  @keyframes slide {
    0% { transform: translateX(0); }
    100% { transform: translateX(-50%); }
  }

  .category-item {
    flex-shrink: 0;
    text-align: center;
    width: 150px;
  }

  .category-item img {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    object-fit: cover;
    margin-bottom: 10px;
  }

  .category-item span {
    font-size: 14px;
    color: #333;
    font-weight: 500;
  }

  .flash-deals {
    background: linear-gradient(135deg, #e3f2fd 0%, #f3e5f5 100%);
    padding: 40px 0;
  }

  .section-header-flash {
    display: flex;
    align-items: center;
    gap: 20px;
    margin-bottom: 30px;
  }

  .section-header-flash h2 {
    font-size: 24px;
    color: #333;
  }

  .section-header-flash span {
    flex: 1;
    font-size: 16px;
    color: #666;
  }

  .deals-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 20px;
  }

  .deal-card {
    background: white;
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    transition: transform 0.2s;
  }

  .deal-card:hover {
    transform: translateY(-4px);
  }

  .product-image {
    position: relative;
    height: 220px;
  }

  .product-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .discount-badge {
    position: absolute;
    top: 10px;
    left: 10px;
    background: #ff4757;
    color: white;
    padding: 4px 8px;
    border-radius: 4px;
    font-size: 12px;
    font-weight: bold;
  }

  .lightning-badge {
    position: absolute;
    top: 10px;
    right: 10px;
    background: #ffd32a;
    color: #333;
    padding: 4px 8px;
    border-radius: 4px;
    font-size: 11px;
    font-weight: 500;
  }

  .product-info {
    padding: 15px;
  }

  .product-info h3 {
    font-size: 14px;
    margin-bottom: 8px;
    color: #333;
    line-height: 1.3;
  }

  .price {
    margin-bottom: 8px;
  }

  .current-price {
    font-size: 18px;
    font-weight: bold;
    color: #ff4757;
  }

  .original-price {
    font-size: 14px;
    color: #999;
    text-decoration: line-through;
    margin-left: 8px;
  }

  .sold-info {
    font-size: 12px;
    color: #666;
  }

  .new-arrivals-section {
    padding: 40px 0;
    background: white;
  }

  .two-column-layout {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 60px;
  }

  .section-header-simple {
    margin-bottom: 20px;
  }

  .section-header-simple h2 {
    font-size: 24px;
    margin-bottom: 5px;
    color: #333;
  }

  .section-header-simple p {
    color: #666;
    font-size: 14px;
    margin-bottom: 15px;
  }

  .products-row {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
  }

  .new-arrival-card {
    background: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  }

  .new-arrival-card img {
    width: 100%;
    height: 120px;
    object-fit: cover;
  }

  .product-details {
    padding: 12px;
  }

  .product-details h4 {
    font-size: 13px;
    margin-bottom: 6px;
    color: #333;
    line-height: 1.2;
  }

  .product-details .price .current {
    font-size: 16px;
    font-weight: bold;
    color: #ff4757;
  }

  .product-details .price .original {
    font-size: 12px;
    color: #999;
    text-decoration: line-through;
    margin-left: 6px;
  }

  .footer {
    background: #333;
    color: white;
    padding: 40px 0 20px;
  }

  .footer-content {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 30px;
    margin-bottom: 30px;
  }

  .footer-section h3 {
    font-size: 16px;
    margin-bottom: 15px;
    color: white;
  }

  .footer-section ul {
    list-style: none;
  }

  .footer-section ul li {
    margin-bottom: 6px;
  }

  .footer-section ul li a {
    color: #ccc;
    text-decoration: none;
    font-size: 14px;
    transition: color 0.2s;
  }

  .footer-section ul li a:hover {
    color: white;
  }

  .social-links {
    display: flex;
    gap: 15px;
  }

  .social-links a {
    font-size: 20px;
    text-decoration: none;
  }

  .payment-section {
    border-top: 1px solid #555;
    padding-top: 20px;
    margin-bottom: 20px;
  }

  .payment-section h3 {
    font-size: 14px;
    margin-bottom: 10px;
    color: white;
  }

  .payment-methods {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
  }

  .payment-methods img {
    height: 25px;
    border-radius: 4px;
  }

  .trustpilot-section {
    text-align: center;
    margin-bottom: 20px;
  }

  .trustpilot-widget {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 15px;
    font-size: 14px;
  }

  .footer-bottom {
    border-top: 1px solid #555;
    padding-top: 15px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 12px;
  }

  .legal-links {
    display: flex;
    gap: 15px;
  }

  .legal-links a {
    color: #ccc;
    text-decoration: none;
  }

  .legal-links a:hover {
    color: white;
  }

  @media (max-width: 768px) {
    .header-info {
      flex-direction: column;
      gap: 10px;
    }

    .left-info {
      flex-direction: column;
      gap: 5px;
    }

    .header-content {
      flex-direction: column;
      gap: 15px;
    }

    .search-bar {
      order: 3;
      max-width: none;
    }

    .nav-menu {
      display: none;
    }

    .slide-content h1 {
      font-size: 28px;
    }

    .categories-track {
      gap: 15px;
    }

    .deals-grid {
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    }

    .two-column-layout {
      grid-template-columns: 1fr;
      gap: 30px;
    }

    .footer-bottom {
      flex-direction: column;
      gap: 10px;
      text-align: center;
    }
  }
</style>
