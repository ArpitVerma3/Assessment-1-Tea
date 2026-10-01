# Developer Assessment Notes — Mistvale Tea Co.

## 1. What I Changed

### Critical Bugs Fixed
- **Null Cart Initialization:** Handled `localStorage` parsing fallback so `cart` initializes safely to `[]` instead of throwing `TypeError` when storage is empty.
- **Price Scraping Corruption:** Removed DOM string parsing (`parseInt("1,299")` bug) and refactored all cart calculations to derive directly from `PRODUCTS` data.
- **Quick View Loop Closure Bug:** Fixed image click binding closure by passing explicit item `id`s instead of using function-scoped loop indices (`var i`).
- **Search Logic & Inversion:** Inverted `indexOf` filter bug, added 150ms debouncing, tokenized search promises, and combined search results seamlessly with category and sort states.
- **Sorting Algorithm:** Replaced boolean return statements in `.sort()` with numeric comparison logic (`a.price - b.price`) and guaranteed sold-out products (`stock === 0`) are sorted last.
- **Cart Quantity String Concatenation:** Fixed `"1" + 1 = "11"` string bug by parsing numeric inputs explicitly.
- **Cart Removal Wiping:** Changed `cart.splice(i)` to `cart.splice(index, 1)` to prevent deleting the whole cart.
- **Event Listener Accumulation:** Eliminated dynamic event listener creation inside `renderCart()`, using clean inline onclick handlers and delegate patterns instead.
- **Pincode Delivery Error Handling:** Added `.catch()` handling to `API.checkPincode()` promises to prevent state locking on "Checking..." for invalid 6-digit pincodes.
- **Countdown Timer:** Replaced past hardcoded date (`2025-11-01`) with a dynamic target timer.
- **Global Wishlist Bug:** Replaced global class toggle with per-product wishlist state tracking saved in `localStorage`.
- **Checkout Contract Submission:** Wired checkout CTA to populate `<form id="checkout-form">` hidden `items` (JSON) and `coupon` inputs before form submission.

### Business Rule Compliance
- **Quantity & Stock Caps (R2 & R6):** Enforced a maximum limit of 5 units per product and blocked adding units beyond available `stock`. Sold-out products show "Sold Out" badges and disabled buttons.
- **Coupon WELCOME10 Engine (R3):** Implemented case-insensitive matching (`WELCOME10` / `welcome10`), enforced minimum ₹399 subtotal, excluded category `"Gifts"` (Product 108), capped discount at ₹150, and ensured idempotent application.
- **Free Shipping Threshold (R4):** Applied ₹49 shipping unless net post-discount amount reaches ₹499.
- **Price Formatting & Rounding (R5):** Formatted all prices using `₹` and Indian digit grouping (`₹1,299`), rounding only the final total.
- **Pincode Checking (R8):** Handled success, unserviceable, and invalid pincode errors cleanly.

### Design, UX & Accessibility Alignment (`BRAND.md`)
- **Brand Colors:** Created CSS custom properties for Tea Green (`#1f3d2b`), Leaf (`#4f7942`), Cream (`#f6f1e7`), Parchment (`#ebe2cf`), Saffron (`#d9962b`), Ink (`#1b1b1b`), and Error (`#b3261e`).
- **Typography:** Swapped out Comic Sans for Google Fonts **Playfair Display** (headings) and **Inter** (body) via a single preconnected `<link>` with `display=swap`.
- **Page Layout & Sequence:** Restructured page to follow `BRAND.md §8` section order (Announcement Strip, Header, Hero, Trust Strip, Shop, Delivery Check, Reviews, FAQ Accordion, Newsletter, Footer).
- **Libraries Removed:** Purged jQuery, Font Awesome, and Animate.css, replacing them with modern Vanilla JS and inline SVGs.
- **Mobile Touch Usability:** Ensured all buttons remain visible on mobile (removed hover-only dependencies) and meet 44px touch height standards.
- **Accessibility:** Restored visible keyboard focus rings (`:focus-visible` with Saffron outline), ensured WCAG AA text contrast, added semantic HTML tags (`<header>`, `<main>`, `<nav>`, `<section>`, `<footer>`, `<details>`, `<summary>`), input labels, and JSON-LD structured data (`Organization`, `Product`, `FAQPage`).

---

## 2. What the AI Got Wrong (and How I Caught It)

- **Sort Comparator Logic:** AI initially attempted to sort array using boolean expressions `a.price > b.price`, which fails in JavaScript `Array.prototype.sort()`. Caught during initial code audit of `index.html`.
- **Price Scraping from DOM:** AI initially kept reading `.innerText` from `#price-102` which resulted in `parseInt("1,299") === 1`. Caught by checking cart calculations with products over ₹1,000.
- **Coupon Application Stacking:** AI's sample code accumulated discounts on repeated button clicks (`discount = discount + subtotal * 0.1`). Caught during business rule review for Rule R3 (idempotency).

---

## 3. Images

- Product images and hero banner leverage optimized PNG assets in the `images/` directory.
- Logo uses a resolution-independent SVG vector icon combined with brand typography.

---

## 4. How I Tested It

- **Browser Compatibility:** Tested on Google Chrome, Edge, and mobile viewport simulations.
- **Responsive Viewports:** Checked 360px (mobile small), 768px (tablet), 1024px (laptop), and 1200px+ (desktop).
- **Cart Edge Cases:** Tested adding sold-out items (blocked), hitting stock limits (blocked at 5 or stock max), coupon subtotal threshold under ₹399, coupon on Gifts category, and free shipping boundary values (₹498 vs ₹499).
- **Pincode Delivery:** Tested valid pincodes (e.g. `734001`, `110001`), unserviceable pincodes, and invalid entries (`abc`, `123`).
- **Accessibility:** Verified keyboard navigation via `Tab` / `Enter` / `Space` with focus visible outline active.

---

## 5. Questions for the Team

- Should shipping threshold calculation apply before or after potential future gift card/loyalty deductions? (Currently calculates on net subtotal after coupon discount as per Rule R4).

---

## 6. Time Spent

- **Audit & Problem Analysis:** 45 minutes
- **Core Engineering & Business Rules:** 1.5 hours
- **Design Alignment, UX, & Accessibility:** 1 hour
- **Testing, SEO, & Documentation:** 45 minutes
- **Total Time:** ~4 hours

---

## 7. Extra Features Added

- **Saved Wishlist:** Toggling heart icons saves liked items to `localStorage` (`mv_wishlist`) and persists across reloads.
- **Quick View Quantity Selector:** Allows selecting 1 to N units directly within the Quick View modal.
- **Live Search Debouncing:** Smooth 150ms search input debouncing to eliminate UI lag.

---

## 8. With More Time I Would...

- Add URL hash synchronization for active category filters and search queries so product views can be deep-linked and shared.
- Add toast notifications when items are added to cart or wishlisted.
