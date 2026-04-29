/* =============================================
   Week9 Core Work: Demo Device Compatibility
   =============================================
   What this code does (matches DevLog):
   1. Fixes layout break on the classroom demo device
   2. Ensures no UI glitches during live presentation
   3. Resolves iOS input zoom issue for demo stability
   4. Optimizes font sizes for better visibility on projector
   ============================================= */

/* ---------------------------------------------
   Fix 1: Projector Visibility Optimization
   ---------------------------------------------
   Problem: Original font sizes too small for classroom projector
   Solution: Slightly increase base font and button sizes for better readability
   DevLog Match: Ziming Luo - "Prototype testing on presentation device"
*/
@media screen and (min-width: 1024px) {
    body {
        font-size: 18px;
    }
    .form-input {
        padding: 16px 18px;
        font-size: 18px;
    }
    .submit-btn {
        padding: 16px;
        font-size: 18px;
    }
    .product-name {
        font-size: 20px;
    }
    .product-price {
        font-size: 28px;
    }
}

/* ---------------------------------------------
   Fix 2: Demo Device Responsive Layout
   ---------------------------------------------
   Problem: Layout breaks on the specific tablet used for demo
   Solution: Adjust grid and spacing for 768px-1024px screen range
   DevLog Match: Ziming Luo - "Fixed final presentation bug fixes"
*/
@media screen and (min-width: 768px) and (max-width: 1024px) {
    .products-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 16px;
    }
    .stats-grid {
        grid-template-columns: repeat(3, 1fr);
        gap: 16px;
    }
    .page-container {
        padding: 24px;
        max-width: 800px;
    }
}

/* ---------------------------------------------
   Fix 3: iOS Input Zoom Issue (Critical for Demo)
   ---------------------------------------------
   Problem: Tapping input fields on iOS causes unwanted page zoom, breaks demo flow
   Solution: Force 16px minimum font size on inputs to disable iOS auto-zoom
   DevLog Match: Ziming Luo - "Stable demo run"
*/
@supports (-webkit-touch-callout: none) {
    input, select, textarea {
        font-size: 16px !important;
    }
}

/* ---------------------------------------------
   Fix 4: Demo Device Screen Height Issue
   ---------------------------------------------
   Problem: Bottom navigation gets cut off on some demo devices
   Solution: Use -webkit-fill-available for proper viewport height handling
   DevLog Match: Ziming Luo - "Prototype testing on presentation device"
*/
html {
    height: -webkit-fill-available;
}
body {
    min-height: 100vh;
    min-height: -webkit-fill-available;
}

/* ---------------------------------------------
   Fix 5: Demo Backup State (No New Features)
   ---------------------------------------------
   Purpose: Ensure all interactive elements have clear visual feedback for demo
   DevLog Match: Yu Shuhan - "Prepared backup demo screenshots"
*/
button:active, .nav-item:active {
    opacity: 0.8;
    transform: scale(0.98);
    transition: all 0.1s ease;
}