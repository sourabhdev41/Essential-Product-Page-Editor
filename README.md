# Essential Product Page Editor

Elementor addon for WooCommerce that lets you fully design a **Quantity + Add to Cart + Buy Now** block — colors, fonts, borders, corner radius, width, height, spacing — with your choice of **Native WooCommerce Checkout** or a **Custom URL** redirect for Buy Now.

Built by **NRW India** — [wp.nrwone.in](https://wp.nrwone.in)

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Requires PHP](https://img.shields.io/badge/PHP-%3E%3D7.4-777bb4)
![Requires WordPress](https://img.shields.io/badge/WordPress-%3E%3D5.8-21759b)
![Requires Elementor](https://img.shields.io/badge/Elementor-required-92003b)
![Requires WooCommerce](https://img.shields.io/badge/WooCommerce-required-96588a)
![License](https://img.shields.io/badge/license-GPLv2%2B-green)

---

## What it does

Drag one Elementor widget — **Add to Cart / Buy Now** — onto any Single Product template (Elementor Theme Builder / Pro, or a product page built with Elementor) and you get:

- A **Quantity stepper** (`−` / number / `+`), transparent by default, with min / max / step / default all configurable
- An **Add to Cart** button — optional AJAX (no page reload), with a choice of what happens after adding: stay on page, go to cart, go to checkout, or a custom URL
- A **Buy Now** button — adds the product to the cart, then redirects straight to the **Native WooCommerce Checkout** or any **Custom URL** you specify
- A **Buttons Order** switch — show Buy Now first or Add to Cart first, without touching the layout
- Fully **responsive**: side-by-side buttons on desktop/tablet, automatically stacked full-width on mobile; quantity always stays above the buttons
- Independent **Style controls** for the Quantity box, Add to Cart button, and Buy Now button:
  - Typography (font family, size, weight, line-height, letter-spacing)
  - Text & background color, with separate Normal / Hover states
  - Border (width, style, color) + independent per-corner radius
  - Box shadow
  - Padding, margin, width, height, gap
- Auto-updates straight from this GitHub repository

## Screenshots

| Default look | Editing in Elementor |
|---|---|
| Pill quantity stepper + Buy Now / Add to Cart buttons | Full Style tab: colors, borders, radius, spacing |

*(Add your own screenshots to a `/screenshots` folder and reference them here.)*

## Requirements

- WordPress 5.8+
- PHP 7.4+
- [WooCommerce](https://wordpress.org/plugins/woocommerce/) (active)
- [Elementor](https://wordpress.org/plugins/elementor/) free or Pro (active)

## Installation

### From a release (recommended)

1. Go to [Releases](../../releases) and download the latest `essential-product-page-editor.zip`.
2. In your WordPress admin, go to **Plugins → Add New → Upload Plugin**.
3. Choose the downloaded zip and click **Install Now**, then **Activate**.

### Manually

1. Clone or download this repository.
2. Copy the `essential-product-page-editor` folder into `wp-content/plugins/`.
3. Activate **Essential Product Page Editor** from **Plugins** in wp-admin.

## Usage

1. Edit a Single Product template with Elementor (via **Templates → Theme Builder → Single Product** if you're using Elementor Pro), or edit a product page directly with Elementor.
2. In the widget panel, open the **Essential Product Page Editor** category.
3. Drag the **Add to Cart / Buy Now** widget onto the page.
4. Configure it under the **Content** tab:
   - **Layout** — direction, button order, quantity position, gap, alignment
   - **Quantity Settings** — show/hide, default/min/max/step
   - **Add to Cart Settings** — text, AJAX toggle, post-add redirect
   - **Buy Now Settings** — text, checkout destination (native or custom URL)
5. Style each part independently under the **Style** tab (Quantity Box / Add to Cart Button / Buy Now Button).

> The widget only renders on an actual WooCommerce product context — a real product page, or a Single Product template being edited/previewed with a product loaded.

## How Buy Now works

Buy Now is not a native WooCommerce feature, so this plugin implements it directly:

1. Clicking **Buy Now** submits the product ID, quantity, and a nonce.
2. A `wp_loaded` hook (priority 30, after WooCommerce's own cart handler) verifies the nonce, adds the item to the cart via `WC()->cart->add_to_cart()`.
3. The customer is redirected to `wc_get_checkout_url()` (Native Checkout) or the Custom URL you configured, via `wp_safe_redirect()`.

Add to Cart, by contrast, can use WooCommerce's standard form submit or its built-in AJAX add-to-cart flow, depending on the **Add via AJAX** toggle.

## Updates

This plugin ships with [Plugin Update Checker](https://github.com/YahnisElsts/plugin-update-checker) wired to:

```
https://github.com/sourabhdev41/essential-product-page-editor
```

To publish an update:

1. Bump the `Version:` header in `essential-product-page-editor.php`.
2. Commit and push to the `main` branch (or tag a release — see `getVcsApi()->enableReleaseAssets()` in the main plugin file if you prefer distributing a built zip per release instead of a branch snapshot).
3. Sites running the plugin will see the update in **Dashboard → Updates** like any WordPress.org plugin.

## Project structure

```
essential-product-page-editor/
├── essential-product-page-editor.php   # Plugin bootstrap, update checker, Buy Now handler
├── includes/
│   ├── class-epe-cart-buy-widget.php   # The Elementor widget (controls + render)
│   └── puc/                            # Plugin Update Checker library
├── assets/
│   ├── css/style.css                   # Front-end styles (defaults + responsive)
│   └── js/script.js                    # Quantity stepper + AJAX add-to-cart
└── readme.txt                          # WordPress.org-style plugin readme
```

## Contributing

Issues and pull requests are welcome. Please open an issue describing the bug or feature before submitting a large PR.

## License

GPLv2 or later, in keeping with the WordPress plugin ecosystem. See [license.txt](includes/puc/license.txt) for the bundled library's license; the plugin's own code is GPLv2+.

## Credits

Developed by **NRW India** — [wp.nrwone.in](https://wp.nrwone.in)
Update checker: [Plugin Update Checker by Yahnis Elsts](https://github.com/YahnisElsts/plugin-update-checker)
