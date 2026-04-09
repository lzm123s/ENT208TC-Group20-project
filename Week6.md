# Week 6 - Page Integration & Navigation Implementation
Project: Lab Eats (Campus Mutual-Aid)
Group 20 | Date: 10/04/2026

## What We Did This Week
Yan Tong: Reviewed core module business processes, coordinated overall prototype planning.
Yu Shuhan: Unified interface visual style, optimized navigation jump logic.
Ziming Luo: Integrated all front-end pages, implemented cross-page navigation and routing.
Rui Chen: Improved database structure, added foreign keys and table constraints.
Yunyi Wang: Completed full wallet process design, recharge/query/record logic.
Yuxuan Xu: Organized project documents, archived weekly outputs and evidence.

## Core Deliverables
1. Cross-page navigation between login, profile, product list, wallet pages
2. Unified global routing and navigation component
3. Database table relationship optimization
4. Full visual style unification across all pages
5. Wallet module full process logic documentation

---

## Navigation Integration Code (Week6 Core Work)
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lab Eats - Global Navigation</title>
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
            --error: #ff5252;
        }
        body {
            background: var(--bg);
            min-height: 100vh;
            color: var(--white);
            padding-bottom: 80px;
        }
        /* Global Navigation Bar (Week6 New) */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            background: var(--card);
            display: flex;
            justify-content: space-around;
            padding: 12px 0;
            border-top: 1px solid #3a3a45;
        }
        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            color: var(--gray);
            text-decoration: none;
            font-size: 12px;
        }
        .nav-item.active {
            color: var(--primary);
        }
        .nav-icon {
            font-size: 20px;
        }
        .page-container {
            padding: 20px;
            max-width: 600px;
            margin: 0 auto;
        }
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        .logo {
            font-size: 24px;
            font-weight: 700;
        }
        .logo .lab { color: var(--primary); }
        .logo .eats { color: var(--white); }
    </style>
</head>
<body>
    <div class="page-container">
        <div class="header">
            <div class="logo">
                <span class="lab">Lab</span>
                <span class="eats">Eats</span>
            </div>
            <div style="color: var(--error); font-weight: 600;">Balance: 0.00€</div>
        </div>
    </div>

    <!-- Week6 Core: Global Navigation Bar -->
    <div class="bottom-nav">
        <a href="index.html" class="nav-item active">
            <div class="nav-icon">🏠</div>
            <span>Home</span>
        </a>
        <a href="products.html" class="nav-item">
            <div class="nav-icon">🛒</div>
            <span>Shop</span>
        </a>
        <a href="wallet.html" class="nav-item">
            <div class="nav-icon">💳</div>
            <span>Wallet</span>
        </a>
        <a href="profile.html" class="nav-item">
            <div class="nav-icon">👤</div>
            <span>Profile</span>
        </a>
    </div>

    <script>
        // Week6: Navigation Active State Logic
        const currentPath = window.location.pathname.split('/').pop();
        const navItems = document.querySelectorAll('.nav-item');
        navItems.forEach(item => {
            if (item.getAttribute('href') === currentPath) {
                navItems.forEach(i => i.classList.remove('active'));
                item.classList.add('active');
            }
        });
    </script>
</body>
</html>