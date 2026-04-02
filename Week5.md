# Week 5 - User & Product Module Development
Project: Lab Eats (Campus Mutual-Aid)
Group 20 | Date: 03/04/2026

## What We Did This Week
| Who | Did What |
|------|------|
| Yan Tong | Confirmed user profile and product list module requirements, adjusted business logic |
| Yu Shuhan | Finalized user center and product page UI details, confirmed component reuse rules |
| Ziming Luo | Implemented user center page and product list page, added basic interaction logic |
| Rui Chen | Completed user login/registration interface docking, basic product data interface development |
| Yunyi Wang | Defined wallet balance display rules, prepared error state prompts |
| Yuxuan Xu | Organized weekly meeting records, updated dev log and evidence |

## Core Deliverables
1.  User center page UI framework (matches the provided screenshot)
2.  Product list page with category filtering and search UI
3.  Basic user login/registration interface docking
4.  Product category and list data display logic

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lab Eats - Profile</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, sans-serif;
        }
        :root {
            --bg: #1a1c23;
            --card: #252730;
            --white: #fff;
            --gray: #a0a0b0;
            --error: #ff5252;
            --primary: #7c7cff;
            --success: #2ecc71;
            --blue: #3498db;
        }
        body {
            background: var(--bg);
            min-height: 100vh;
            padding: 20px;
            color: var(--white);
        }
        .profile-container {
            max-width: 600px;
            margin: 0 auto;
            text-align: center;
        }
        .username {
            font-size: 32px;
            font-weight: 600;
            margin-bottom: 8px;
        }
        .balance-text {
            color: var(--gray);
            margin-bottom: 20px;
        }
        .alert-bar {
            background: var(--error);
            padding: 16px;
            border-radius: 12px;
            margin-bottom: 30px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 16px;
            margin-bottom: 30px;
        }
        .stat-card {
            background: var(--card);
            padding: 20px;
            border-radius: 12px;
        }
        .stat-icon {
            font-size: 28px;
            margin-bottom: 10px;
        }
        .stat-value.rank { color: var(--primary); font-size: 32px; font-weight: 700;}
        .stat-value.purchase { color: var(--success); font-size: 32px; font-weight: 700;}
        .stat-value.procurement { color: var(--blue); font-size: 32px; font-weight: 700;}
        .stat-label {
            color: var(--gray);
            font-size: 14px;
            margin-top: 8px;
        }
        .info-section {
            text-align: left;
        }
        .info-title {
            color: var(--gray);
            font-size: 18px;
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .info-item {
            background: var(--card);
            padding: 16px;
            border-radius: 8px;
            margin-bottom: 16px;
        }
        .info-value {
            font-size: 16px;
            margin-bottom: 6px;
        }
        .info-desc {
            color: var(--gray);
            font-size: 12px;
        }
    </style>
</head>
<body>
    <div class="profile-container">
        <div class="username">ziming.luo</div>
        <div class="balance-text">Your balance: 0.00€</div>

        <div class="alert-bar">
            <span>⚠️</span>
            <span>Your account does not have enough balance! Top up to join the next group orders.</span>
        </div>

        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-icon">🏆</div>
                <div class="stat-value rank">#2</div>
                <div class="stat-label">Balance ranking</div>
            </div>
            <div class="stat-card">
                <div class="stat-icon">🛒</div>
                <div class="stat-value purchase">0.00€</div>
                <div class="stat-label">Items bought</div>
            </div>
            <div class="stat-card">
                <div class="stat-icon">📦</div>
                <div class="stat-value procurement">0.00€</div>
                <div class="stat-label">Bought for LabEats</div>
            </div>
        </div>

        <div class="info-section">
            <div class="info-title">ℹ️ Profile information</div>
            <div class="info-item">
                <div class="info-value">ziming.luo</div>
                <div class="info-desc">Your username is synced from AD</div>
            </div>
        </div>

        <div class="info-section" style="margin-top: 20px;">
            <div class="info-title">Debug information</div>
        </div>
    </div>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lab Eats - Products</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, sans-serif;
        }
        :root {
            --bg: #1a1c23;
            --card: #252730;
            --white: #fff;
            --gray: #a0a0b0;
            --primary: #7c7cff;
        }
        body {
            background: var(--bg);
            min-height: 100vh;
            padding: 20px;
            color: var(--white);
        }
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        .header-title {
            font-size: 24px;
            font-weight: 600;
        }
        .header-right {
            display: flex;
            align-items: center;
            gap: 16px;
        }
        .balance-badge {
            color: var(--error);
            font-weight: 600;
        }
        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--primary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
        }
        .search-bar {
            margin-bottom: 20px;
        }
        .search-input {
            width: 100%;
            padding: 14px 16px;
            background: var(--card);
            border: 1px solid #3a3a45;
            border-radius: 8px;
            color: var(--white);
            font-size: 16px;
        }
        .category-filter {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-bottom: 20px;
        }
        .category-tag {
            background: var(--primary);
            color: var(--white);
            padding: 8px 12px;
            border-radius: 8px;
            font-size: 14px;
        }
        .category-tag.unselected {
            background: transparent;
            border: 1px solid var(--gray);
            color: var(--gray);
        }
        .products-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 16px;
        }
        .product-card {
            background: var(--card);
            padding: 16px;
            border-radius: 12px;
        }
        .product-category {
            color: var(--gray);
            font-size: 12px;
            margin-bottom: 8px;
        }
        .product-name {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 10px;
        }
        .product-price {
            font-size: 24px;
            font-weight: 700;
            color: var(--primary);
            margin-bottom: 16px;
        }
        .buy-btn {
            width: 100%;
            padding: 12px;
            background: var(--primary);
            border: none;
            border-radius: 8px;
            color: #000;
            font-weight: 600;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div style="display: flex; align-items: center; gap: 16px;">
                <span>☰</span>
                <div class="header-title">Lab Eats</div>
            </div>
            <div class="header-right">
                <div class="balance-badge">⚠️ 0.00€</div>
                <div class="user-avatar">Z</div>
            </div>
        </div>

        <div class="search-bar">
            <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
                <span style="color: var(--gray);">Product search</span>
                <span style="color: var(--gray); font-size: 14px;">24 products found</span>
            </div>
            <input type="text" class="search-input" placeholder="Search products...">
        </div>

        <div class="category-filter">
            <div style="display: flex; justify-content: space-between; width: 100%; margin-bottom: 8px;">
                <span style="color: var(--gray);">Filter categories</span>
                <div>
                    <button style="background: var(--card); border: none; color: var(--white); padding: 4px 8px; border-radius: 4px;">Select all</button>
                    <button style="background: transparent; border: none; color: var(--gray); padding: 4px 8px; border-radius: 4px;">Clear all</button>
                </div>
            </div>
            <div class="category-tag">Cold Drinks 7</div>
            <div class="category-tag">Hot Drinks 3</div>
            <div class="category-tag">Snacks 5</div>
            <div class="category-tag">Instant Food 3</div>
            <div class="category-tag">Frozen Food 2</div>
            <div class="category-tag">Fresh Fruit 2</div>
            <div class="category-tag">Bakery 1</div>
            <div class="category-tag">Breakfast 1</div>
            <div class="category-tag unselected">Office Supplies 3</div>
            <div class="category-tag unselected">Personal Care 3</div>
        </div>

        <div class="products-grid">
            <div class="product-card">
                <div class="product-category">Hot Drinks</div>
                <div class="product-name">Americano (Machine)</div>
                <div class="product-price">19.45€ <span style="font-size: 14px; color: var(--gray);">(5.5€ + 13.95€)</span></div>
                <button class="buy-btn">Buy</button>
            </div>
            <div class="product-card">
                <div class="product-category">Fresh Fruit</div>
                <div class="product-name">Apple (1pc)</div>
                <div class="product-price">8.85€ <span style="font-size: 14px; color: var(--gray);">(3.5€ + 5.35€)</span></div>
                <button class="buy-btn">Buy</button>
            </div>
            <div class="product-card">
                <div class="product-category">Fresh Fruit</div>
                <div class="product-name">Banana (1pc)</div>
                <div class="product-price">5.60€ <span style="font-size: 14px; color: var(--gray);">(2.2€ + 3.40€)</span></div>
                <button class="buy-btn">Buy</button>
            </div>
            <div class="product-card">
                <div class="product-category">Bakery</div>
                <div class="product-name">Butter Croissant</div>
                <div class="product-price">18.20€ <span style="font-size: 14px; color: var(--gray);">(6€ + 12.20€)</span></div>
                <button class="buy-btn">Buy</button>
            </div>
        </div>
    </div>
</body>
</html>