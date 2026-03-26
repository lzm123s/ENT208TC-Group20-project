# Week 4 - Frontend Project Structure & Login Page Framework
Project: Lab Eats (Campus Mutual-Aid)
Group 20 | Date: 27/03/2026

## Project Status: 🟢 ON TRACK
Traffic light (RYG — this week):
🟢 Green: First local front-end structure; basic login page framework; homepage rough + image direction; requirements and initial DB field planning advanced.
🟡 Yellow: Final branded homepage art not locked (temporary hero image); navigation still early-stage.
🔴 Red: No cross-module end-to-end flow testable yet; wallet still in early specification vs integrated UI.

## What We Did This Week (100% Match DevLog)
| Who | Did What |
|------|------|
| Yan Tong | Followed confirmed scope; sorted basic user requirements and simple business rules per module. |
| Yu Shuhan | Used AI to generate initial core page sketches; planned overall layout and basic navigation logic. |
| Ziming Luo | Built local project file structure; implemented basic login page framework for front-end prep. |
| Rui Chen | Designed simple base data structures; initial DB field planning for user information. |
| Yunyi Wang | Captured wallet module basics; preliminary notes for simulated payment behaviour. |
| Yuxuan Xu | Recorded weekly meeting content, collected progress, organised Week 4 dev log documents and evidence. |

## Core Deliverables This Week
1.  Local front-end project folder structure built, unified naming convention confirmed
2.  1:1 basic login page framework implemented (matches UI design draft)
3.  Tab navigation entry reserved for Register/Reset Password pages
4.  Initial user information database table field planning completed
5.  Global style specification confirmed for subsequent page development

---

## 1. Login Page Framework Code (Week4 Scope: Static UI + Minimal Tab Switch)
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lab Eats - Sign In</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
        }

        /* Global Style (Week4: Unified Specification Confirmed) */
        :root {
            --primary-color: #7c7cff;
            --bg-dark: #1a1c23;
            --card-bg: #252730;
            --text-white: #ffffff;
            --text-gray: #a0a0b0;
            --error-color: #ff5252;
            --border-color: #3a3a45;
        }

        body {
            background-color: var(--bg-dark);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .login-container {
            width: 100%;
            max-width: 600px;
            text-align: center;
        }

        /* App Title */
        .app-title {
            font-size: 64px;
            font-weight: 700;
            margin-bottom: 16px;
        }
        .app-title .lab {
            color: var(--primary-color);
        }
        .app-title .eats {
            color: var(--text-white);
        }

        .welcome-text {
            color: var(--text-white);
            font-size: 22px;
            margin-bottom: 40px;
            opacity: 0.9;
        }

        /* Tab Bar (Week4: Navigation Entry Reserved) */
        .tab-bar {
            display: flex;
            background-color: var(--card-bg);
            border-radius: 12px;
            padding: 4px;
            margin-bottom: 24px;
        }
        .tab-btn {
            flex: 1;
            padding: 12px 0;
            background: transparent;
            border: none;
            border-radius: 8px;
            color: var(--text-gray);
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        .tab-btn.active {
            background-color: var(--primary-color);
            color: var(--text-white);
        }

        /* Error Alert (UI Framework Only, No Trigger Logic in Week4) */
        .error-alert {
            background-color: var(--error-color);
            border-radius: 12px;
            padding: 16px 20px;
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 24px;
            text-align: left;
        }
        .error-alert .error-icon {
            width: 20px;
            height: 20px;
            border-radius: 50%;
            border: 2px solid #000000;
            color: #000000;
            font-weight: 700;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-shrink: 0;
        }
        .error-alert .error-text {
            color: var(--text-white);
            font-size: 16px;
            line-height: 1.4;
        }

        /* Form Input Framework */
        .form-group {
            margin-bottom: 24px;
            text-align: left;
        }
        .form-label {
            display: block;
            color: #e0e0e0;
            font-size: 16px;
            margin-bottom: 8px;
        }
        .form-input {
            width: 100%;
            padding: 14px 16px;
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            color: var(--text-white);
            font-size: 16px;
            outline: none;
        }
        .form-input.error {
            border-color: var(--error-color);
        }
        .input-hint {
            color: var(--error-color);
            font-size: 14px;
            margin-top: 6px;
        }

        /* Submit Button */
        .submit-btn {
            width: 100%;
            padding: 16px;
            background-color: var(--primary-color);
            border: none;
            border-radius: 8px;
            color: #000000;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="login-container">
        <!-- App Title -->
        <h1 class="app-title">
            <span class="lab">Lab</span>
            <span class="eats">Eats</span>
        </h1>
        <p class="welcome-text">Welcome! Please sign in.</p>

        <!-- Tab Bar: Navigation Reserved (Week4 Scope) -->
        <div class="tab-bar">
            <button class="tab-btn active">Email + Password</button>
            <button class="tab-btn">Register</button>
            <button class="tab-btn">Reset Password</button>
        </div>

        <!-- Error Alert: UI Framework Only -->
        <div class="error-alert">
            <span class="error-icon">✕</span>
            <div class="error-text">Sign-in failed. Please check your credentials.</div>
        </div>

        <!-- Login Form: Basic Framework (Week4 Scope) -->
        <form id="loginForm">
            <div class="form-group">
                <label class="form-label">Email address</label>
                <input 
                    type="email" 
                    class="form-input" 
                    value="demo.admin@labeats.local"
                    placeholder="Enter your campus email"
                >
            </div>

            <div class="form-group">
                <label class="form-label">Password</label>
                <input 
                    type="password" 
                    class="form-input error" 
                    placeholder="Enter your password"
                >
                <p class="input-hint">Password is required</p>
            </div>

            <button type="button" class="submit-btn">Sign in with email</button>
        </form>
    </div>

    <!-- Week4 Minimal JS: Only Tab Switch, No Form Validation/Submit Logic (No Over-Scope) -->
    <script>
        const tabBtns = document.querySelectorAll('.tab-btn');
        tabBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                tabBtns.forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
            });
        });
    </script>
</body>
</html>


2. Initial User Database Field Planning

-- Week4: Initial User Table Field Planning (Rui Chen's Work)
-- Lab Eats Campus Mutual-Aid App
-- Date: 27/03/2026

CREATE TABLE IF NOT EXISTS `lab_eats_users` (
    `user_id` INT PRIMARY KEY AUTO_INCREMENT COMMENT 'Unique user ID',
    `campus_email` VARCHAR(100) NOT NULL UNIQUE COMMENT 'Campus email for login',
    `password_hash` VARCHAR(255) NOT NULL COMMENT 'Encrypted password storage',
    `full_name` VARCHAR(50) DEFAULT NULL COMMENT 'User full name',
    `student_id` VARCHAR(20) DEFAULT NULL UNIQUE COMMENT 'Campus student ID',
    `phone_number` VARCHAR(20) DEFAULT NULL COMMENT 'Contact phone number',
    `avatar_url` VARCHAR(255) DEFAULT NULL COMMENT 'User avatar link',
    `account_status` TINYINT DEFAULT 1 COMMENT '1: Active, 0: Disabled',
    `create_time` DATETIME DEFAULT CURRENT_TIMESTAMP COMMENT 'Account creation time',
    `update_time` DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT 'Last update time'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='Week4 Initial User Information Table';