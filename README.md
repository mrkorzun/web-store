# 🛒 Full-Stack Online Store

An individual project focused on building a fully functional online store
powered by the **DummyJSON API**.  
The application implements modern front-end patterns including asynchronous data
handling, dynamic filtering, keyword search, persistent state management, and a
responsive user interface with light/dark theming.

This project was developed as part of an intensive JavaScript learning program
and demonstrates practical skills in working with REST APIs, modular
architecture, and browser storage.

---

## 🌐 Live Demo

👉 [**View the live project**](https://mrkorzun.github.io/web-store/)

---

## ✅ Roadmap

📋 [**View the full Technical Specification (TZ)**](./TZ.md)

- [x] Environment setup and project file structure
- [ ] Rendering the category and product lists on the home page
- [ ] Search and category filtering implementation
- [ ] Modal window and product-by-ID logic
- [ ] LocalStorage integration for the cart and wishlist
- [ ] Wishlist and Cart pages
- [ ] Final styling polish and dark theme
- [ ] Deployment to GitHub Pages

---

## 🚀 Core Features

### 🗂️ Product Catalog

Loads products from the API with built-in pagination (12 items per page) and a
**"Load More"** button for seamless browsing. When no more products are
available, the button is hidden and a notification is displayed to the user.

### 🔍 Search & Filtering

- **Keyword search** across the entire product database via the header search
  form.
- **Category filtering** with dynamic highlighting of the currently active
  category.
- Empty-query protection prevents unnecessary API calls.
- A dedicated clear button instantly resets the search and restores the full
  product list.
- Friendly "not found" messaging when no products match the query.

### ❤️ Wishlist

Users can save favorite products to their personal wishlist. All data is
persisted in `localStorage`, so the list survives page reloads and browser
restarts. A counter in the navigation bar reflects the number of saved items in
real time.

### 🛒 Shopping Cart

- Add and remove products from the cart with a single click.
- Automatic calculation of the **total item count (Items)** and **final price
  (Total)**.
- Cart state is fully persisted in `localStorage`.
- A **"Buy Products"** button triggers a confirmation notification on checkout.

### 🪟 Product Details Modal

- Clicking any product card opens a detailed modal window.
- Fetches full product data by ID from the API.
- Smartly detects whether the product is already in the cart/wishlist and
  updates button text accordingly (**Add** ↔ **Remove**).
- Closes on backdrop click, close button, or the **ESC** key.
- Keyboard listeners are attached/detached dynamically to optimize performance.

### 🎨 UI / UX Enhancements

- 🌗 **Light and dark theme** toggle with preference saved in `localStorage`.
- ⏳ **Loading indicator** during API requests.
- ⬆️ **Scroll-to-top button** for easy navigation on long product lists.
- 🔔 **Toast notifications** via `iziToast` for smooth user feedback.
- 📱 **Responsive layout** adapted for mobile, tablet, and desktop.

---

## 🔗 API Endpoints

The project uses the following endpoints from
[DummyJSON](https://dummyjson.com/docs/products):

| Method | Endpoint                     | Description                                         |
| ------ | ---------------------------- | --------------------------------------------------- |
| `GET`  | `/products`                  | Fetch all products with pagination support          |
| `GET`  | `/products/{id}`             | Fetch detailed information about a specific product |
| `GET`  | `/products/search?q={query}` | Search for products by keyword                      |
| `GET`  | `/products/category-list`    | Retrieve the list of all available categories       |
| `GET`  | `/products/category/{name}`  | Fetch products filtered by a specific category      |

Pagination is handled via the `limit` and `skip` query parameters:

```js
const url = `https://dummyjson.com/products?limit=12&skip=${(currentPage - 1) * 12}`;
```

---

## 🛠 Tech Stack

- **JavaScript (ES6+)** — modular architecture using native `import` / `export`
  syntax.
- **HTML5** — semantic, accessible markup.
- **CSS3** — modern layout techniques (Flexbox, Grid), CSS variables for
  theming.
- **Vite** — lightning-fast development server and optimized production builds.
- **DummyJSON API** — free public REST API for testing and prototyping.
- **iziToast** — lightweight notification library for clean user feedback.
- **Git & GitHub** — version control and collaborative workflow.

---

## 📁 Modular JS Structure

The codebase is split into independent modules, making it easy to maintain,
test, and scale:

| File                  | Responsibility                                        |
| --------------------- | ----------------------------------------------------- |
| `home.js`             | Logic for the Home page (`index.html`)                |
| `wishlist.js`         | Logic for the Wishlist page (`wishlist.html`)         |
| `cart.js`             | Logic for the Cart page (`cart.html`)                 |
| `products-api.js`     | All backend communication (fetch requests)            |
| `render-functions.js` | Functions that generate HTML markup for UI elements   |
| `storage.js`          | Utilities for reading and writing `localStorage`      |
| `handlers.js`         | Event handler functions passed to `addEventListener`  |
| `modal.js`            | Modal window controls (open, close, event wiring)     |
| `helpers.js`          | Shared helper utilities used across the project       |
| `refs.js`             | Centralized object holding references to DOM elements |
| `constants.js`        | Reusable constants and configuration values           |

---

## 🗂️ Project Structure

```
web-store/
├── .github/              # GitHub workflows and configs
├── assets/               # Static assets
├── src/
│   ├── css/              # Stylesheets for individual UI sections
│   ├── img/              # Images and icons
│   ├── js/               # JavaScript modules
│   ├── partials/         # Reusable HTML partials
│   ├── public/           # Public static files
│   ├── cart.html         # Cart page
│   ├── cart.js           # Cart page logic
│   ├── home.js           # Home page logic
│   ├── index.html        # Home page
│   ├── wishlist.html     # Wishlist page
│   └── wishlist.js       # Wishlist page logic
├── .editorconfig
├── .gitignore
├── .prettierrc
├── package.json
├── README.md             # You are here
├── TZ.md                 # Technical specification
└── vite.config.js
```

---

## 💻 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) **v18 or higher**
- [npm](https://www.npmjs.com/) **v9 or higher**

### Installation

**1. Clone the repository:**

```bash
git clone https://github.com/mrkorzun/web-store.git
cd web-store
```

**2. Install dependencies:**

```bash
npm install
```

**3. Start the development server:**

```bash
npm run dev
```

The app will be available at [`http://localhost:5173`](http://localhost:5173) by
default.

### Build for Production

```bash
npm run build
```

The optimized output will be generated in the `dist/` folder.

### Preview the Production Build

```bash
npm run preview
```

---

## 💾 LocalStorage Keys

The project uses the following keys to persist user data between sessions:

| Key        | Stores                                       |
| ---------- | -------------------------------------------- |
| `cart`     | Array of product IDs added to the cart       |
| `wishlist` | Array of product IDs added to the wishlist   |
| `theme`    | Currently selected theme (`light` or `dark`) |

---

## 📚 Documentation

- 📋 [**Technical Specification (TZ)**](./TZ.md) — full breakdown of project
  requirements and features.
- 🌐 [**DummyJSON API Docs**](https://dummyjson.com/docs/products) — official
  API documentation.
- 🔔 [**iziToast Documentation**](https://izitoast.marcelo-miranda.dev/) —
  notification library reference.

---

## 👤 Author

**mrkorzun**  
🔗 GitHub: [@mrkorzun](https://github.com/mrkorzun)

---

## 📝 License

This project was created for educational purposes as part of an intensive
JavaScript learning program.  
Feel free to use it as a reference or learning resource.

---

<div align="center">

⭐ **If you found this project useful, please consider giving it a star!** ⭐

</div>
