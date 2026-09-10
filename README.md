# Product Recommendation System for Home Appliances - Implementation Plan

The goal is to build a beautiful, premium e-commerce platform for home appliances. The application features a Content-Based Filtering recommendation engine, a role-based workflow (Customer, Shop Owner, Admin), and order/product management with an approval pipeline.

---

## User Review Required

> [!IMPORTANT]
> **Key Architecture Decisions**
> 1. **Framework & Stack**: We are building a client-side Single Page Application (SPA) using **Vite + Vanilla JavaScript** and **Vanilla CSS**. This ensures maximum responsiveness, visual excellence, and zero setup hassle.
> 2. **Mock Database**: Data will be managed via `localStorage` to persist users, products, orders, and reviews. A comprehensive seed dataset will initialize the platform with high-quality home appliances on first load.
> 3. **Content-Based Filtering**: The recommendation engine runs on the client. It tokenizes, filters stop words, calculates TF (Term Frequency) vectors, and computes **Cosine Similarity** between product descriptions to find recommendations in real time.
> 4. **Role Switcher**: To make review and testing simple, we will include a prominent **Role Switcher** in the header. You can instantly toggle between **Customer**, **Shop Owner**, and **Admin** views to test their respective permissions and flows.

---

## Proposed Changes

We will create a clean and structured directory using Vite's Vanilla template:

```
Product Recommendation system/
├── index.html
├── src/
│   ├── style.css         # Premium dark/slate theme with glassmorphism
│   ├── main.js           # Core router and layout controller
│   ├── db.js             # LocalStorage database logic & seed data
│   ├── recommender.js    # Content-Based Filtering engine (Cosine Similarity)
│   └── components/
│       ├── header.js     # Role switcher & navigation
│       ├── customer.js   # Catalog, cart, details, recommendations, checkout
│       ├── owner.js      # Seller dashboard, add/edit product forms
│       └── admin.js      # Admin review panel, statistics, global product list
```

### 1. Database & Mock Data (`src/db.js`)
We will create a helper module to interact with `localStorage`.
- **Seed Data**: 12+ premium home appliances across categories (Kitchen, Laundry, Living Room/Comfort). Each product will have detailed descriptions, prices, specs, and status (`approved` by default for seed data).
- **Schemas**:
  - `products`: `{ id, name, category, price, description, specs, image, ownerId, status ('pending' | 'approved' | 'rejected'), feedback }`
  - `orders`: `{ id, customerName, items, total, date, status }`
  - `users`: `{ id, username, role ('customer' | 'owner' | 'admin') }`

### 2. Recommendation Engine (`src/recommender.js`)
Content-based recommendation logic:
- **Tokenization**: Extract words from descriptions, lowercase them, and remove punctuation.
- **Stop Word Removal**: Filter out common grammatical terms (e.g., "and", "the", "with", "for").
- **Term Frequency - Inverse Document Frequency (TF-IDF)**: Construct word frequency vectors for each product.
- **Cosine Similarity**: Compare vectors to compute similarity coefficients.
- **Recommendations**: For any given product, sort other *approved* products by similarity score and return the top 4 matches.

### 3. Aesthetics & Design System (`src/style.css`)
We will build a high-fidelity visual experience:
- **Theme**: Premium Dark Slate/Indigo (deep dark backgrounds, soft neon-violet highlights, clean white typography, and glassmorphic card borders).
- **Typography**: Inter (imported from Google Fonts).
- **Interactions**: CSS transitions, hover scales, active button states, and smooth slide-in panels for the cart/forms.
- **Layouts**: Responsive CSS Grid and Flexbox structures.

### 4. Components
- **Header (`src/components/header.js`)**: Navigation links, Cart counter, and the **Role Switcher Dropdown**.
- **Customer Portal (`src/components/customer.js`)**:
  - Grid of approved products.
  - Search bar + Category filter.
  - Product Details Modal showing specifications, description, and "Similar Products" recommendation list.
  - Slide-out Cart and standard Checkout form.
- **Owner Dashboard (`src/components/owner.js`)**:
  - Product lists categorized by approval state (Pending, Approved, Rejected).
  - Stat cards (Total Sales, Active Products).
  - Modal form to add products. New products start as `pending`.
- **Admin Dashboard (`src/components/admin.js`)**:
  - Queue of pending products with action buttons (Approve, Reject with custom feedback).
  - System performance metrics (Total platform sales, user counts).

---

## Verification Plan

### Automated Verification
- We will write test scenarios inside a scratch script (`scratch/test_recommender.js`) and run them with Node.js to verify the recommendation math works accurately.

### Manual Verification
1. Open the application in the browser using the Vite development server.
2. **As Customer**: Browse products, view a product to inspect the recommendation list (ensure it shows relevant appliances), add to cart, and checkout.
3. **As Shop Owner**: Add a new appliance product. Verify it shows as "Pending" and does *not* appear in the customer view.
4. **As Admin**: Go to the Admin dashboard, review the pending product, approve it.
5. **As Customer**: Verify that the newly approved product is now visible in the catalog and starts appearing in recommendations.
