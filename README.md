# HomeRecommend - Smart Home Appliances Product Recommendation System

An intelligent, full-featured eCommerce platform for smart home appliances powered by an in-browser **Content-Based Filtering Vector Recommendation Engine** using Term Frequency and Cosine Similarity.

Built with **Vanilla JavaScript (ES Modules)**, modern **CSS Glassmorphism design**, and **Vite**, featuring a multi-role RBAC architecture (Customer, Shop Owner, Administrator) with client-side state persistence.

---

## 🌟 Key Highlights & Features

### 1. 🧠 Content-Based Recommendation Engine
- **Vector Space Matching**: Recommends appliances based on text description similarity, product category, and key technical specifications.
- **Mathematical Cosine Similarity**:
  $$\text{Cosine Similarity}(A, B) = \frac{A \cdot B}{\|A\| \|B\|} = \frac{\sum_{i=1}^{n} A_i B_i}{\sqrt{\sum_{i=1}^{n} A_i^2} \sqrt{\sum_{i=1}^{n} B_i^2}}$$
- **Natural Language Processing (NLP)**:
  - Text lowercasing and punctuation normalization (preserving hyphenated terms like `eco-friendly`, `wi-fi`).
  - Stop-word filtering removing over 100+ conversational English words.
  - Term Frequency (TF) map computation.
- **Dynamic Similarity Badging**: Shows real-time cosine similarity match percentages (e.g. `✨ 88% Match`) in the product modal recommendations carousel.

### 2. 👥 Multi-Role RBAC System
Switch seamlessly between 3 distinct user personas directly via the navigation header dropdown:

| Persona | Role | Capabilities |
| :--- | :--- | :--- |
| **John Doe** | `customer` | Browse catalog, instant keyword search, category filters, view recommendations, add to cart, adjust quantities, place mock orders, view order receipt. |
| **Appliances Galore Shop** | `owner` | Seller dashboard, view listing statuses (`approved`, `pending`, `rejected`), submit new appliances with custom specifications, edit listings, view admin feedback. |
| **EcoCool Systems** | `owner` | Specialized cooling and comfort appliances merchant panel. |
| **System Administrator** | `admin` | Platform KPI cards (Gross Revenue, Total Orders, Inventory, Sellers), pending approval queue to approve/reject listings with custom seller feedback, inventory audit, recent customer orders transaction ledger. |

### 3. 🛍️ Customer Storefront & Checkout
- **Instant Search & Category Filter**: Filter products by categories (`All`, `Kitchen`, `Laundry`, `Comfort`, `Cleaning`) or live text search.
- **Rich Product Details Modal**: Comprehensive appliance view with high-resolution imagery, categorized technical specs table, and related content-based recommendations.
- **Slide-Over Cart Drawer**: Real-time quantity increment/decrement, line-item removal, free shipping calculations, and subtotal updates.
- **Mock Checkout & Receipt**: Secure checkout form with validation and an instant **Order Confirmation Receipt Modal** generating a unique Order ID and estimated delivery date.

### 4. ⚙️ Merchant & Administrative Workflows
- **Appliance Listing Submission**: Shop owners can list new products with flexible key-value specifications (e.g. `Power: 1200W`, `Capacity: 26 cu. ft.`).
- **Two-Tier Approval Workflow**: All newly added or edited products start in `pending` state and do not appear in the customer storefront until approved by an administrator.
- **Feedback Loop**: When an admin rejects an appliance listing, they can input a feedback message (e.g. "Description too short; please specify voltage"). The merchant sees this feedback bubble highlighted in their seller panel.

---

## 🛠️ Technology Stack

- **Frontend Core**: Vanilla HTML5, Vanilla JavaScript (Modern ES Modules)
- **Styling**: Vanilla CSS3 (Custom Design System, CSS Variables, Glassmorphism, Responsive Grid & Flexbox)
- **Tooling & Bundler**: [Vite](https://vitejs.dev/) (Rapid HMR & optimized production build)
- **Database / State**: LocalStorage abstraction layer with automatic initial data seeding and CustomEvent-driven reactive state updates

---

## 📂 Project Structure

```
Product Recommendation system/
├── index.html                   # Semantic HTML layout, modals, header, footer
├── package.json                 # Project configuration and Vite scripts
├── package-lock.json
├── public/                      # Static public assets
├── src/
│   ├── main.js                  # App bootstrap, view router & event bus
│   ├── db.js                    # LocalStorage database wrapper & seed appliances
│   ├── recommender.js           # NLP tokenization, TF & Cosine Similarity engine
│   ├── style.css                # Dark slate & indigo glassmorphic design system
│   ├── assets/                  # Icons and visual media assets
│   └── components/
│       ├── header.js            # Sticky navigation, role switcher, cart trigger
│       ├── customer.js          # Storefront catalog, modal, cart drawer, checkout
│       ├── owner.js             # Merchant dashboard & product creation modal
│       └── admin.js             # Admin approval queue, inventory audit, orders ledger
└── README.md                    # Project documentation
```

---

## 🚀 Getting Started

### Prerequisites
Make sure you have [Node.js](https://nodejs.org/) installed (version 18 or higher recommended).

### 1. Clone or Open the Project
Open the project directory in your terminal:
```bash
cd "Product Recommendation system"
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Run Development Server
```bash
npm run dev
```
Once started, open your browser and navigate to:
```
http://localhost:5173/
```

### 4. Build for Production
To generate an optimized production bundle:
```bash
npm run build
```

### 5. Preview Production Build
```bash
npm run preview
```

---

## 🧪 Step-by-Step Feature Walkthrough

### Scenario A: Test Content-Based Recommendations
1. Navigate to **Browse Store** as `John Doe (customer)`.
2. Click on the **Smart Inverter French Door Refrigerator** card.
3. Scroll to the bottom of the modal to view the **"Similar Products Recommended For You"** section.
4. Notice similar appliances (e.g. *Retro Style Refrigerator*, *Countertop Microwave Oven*) displayed with calculated similarity badges (e.g. `✨ 78% Match`).
5. Click on any recommended card to immediately navigate to its details and recalculate recommendations in real-time.

### Scenario B: Add to Cart & Checkout
1. Click **Add to Shopping Cart** from the product modal or catalog card.
2. Click the cart icon in the top right header to open the slide-out drawer.
3. Click **Proceed to Checkout**.
4. Fill in the mock shipping address and card details and submit.
5. Receive the **Order Confirmed** receipt modal with your unique Order ID.

### Scenario C: Merchant Listing & Admin Review Workflow
1. In the header user dropdown, switch to **Appliances Galore Shop (owner)**.
2. Notice the **Seller Panel** tab appears in the navigation bar.
3. Click **✚ Add New Product**, enter appliance details (name, category, price, specs, description), and submit.
4. Notice the new product appears with a yellow **`pending`** badge.
5. In the header dropdown, switch to **System Administrator (admin)**.
6. Under the **Pending Approval Queue**, review the new appliance listing.
7. Click **Approve Listing** (or **Reject Listing** with feedback).
8. Switch back to **John Doe (customer)**: the approved appliance is now live in the store catalog!

---

## 📄 License
This project is open source and available under the [MIT License](LICENSE).
