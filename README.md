# Shop

An online shop prototype built with Django 5.1 on top of Colorlib's **Karma Shop** HTML template. Categories and products are managed in the Django admin and rendered on the storefront home page and category pages. The cart and checkout flow is still being built.

## Status

Work in progress (learning project).

- **Works:** catalog management in the admin, the home page "Latest Products" block (8 random products from the database), category product pages, image uploads.
- **Partial:** `/add_to_cart/<id>/` stores product IDs in the session, but the cart page does not display them yet.
- **Not implemented yet:** real product detail pages, checkout and order processing, user sign-up and login. The product, cart, checkout, confirmation, contact and login pages are still static template pages.
- The home page picks 8 random products, so the database must contain at least 8 products. The bundled sample database already has 8.

## Features

- Catalog models: `Category` (with image), `Subcategory`, `Product` (price, availability, description, image), extra product images and video links, plus `ProductReview`, `Order` and `OrderProduct` models for upcoming features
- Django admin with inline product images and videos, and category search
- Storefront pages based on the Karma template: home, category listing, cart, checkout, confirmation, contact
- Session-based add-to-cart endpoint
- Uploaded media served by Django in development

## Tech stack

- Python 3.10+, Django 5.1
- Pillow (for `ImageField`)
- SQLite
- Front end: Karma Shop template (Bootstrap, jQuery, Owl Carousel, SCSS)

## Getting started

### Prerequisites

- Python 3.10 or newer
- pip

### Installation

```bash
git clone https://github.com/Viltrumlik/shop.git
cd shop
python -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate
pip install "Django>=5.1,<5.2" Pillow
```

There is no `requirements.txt` yet; Django and Pillow are the only third-party packages the code uses.

### Configuration

All settings are in `market/settings.py` (no environment variables). It is configured for local development only (`DEBUG = True`, a hard-coded development `SECRET_KEY`). Before deploying anywhere public, set your own secret key, `DEBUG = False` and `ALLOWED_HOSTS`.

### Run

```bash
python manage.py migrate
python manage.py createsuperuser   # to log in to the admin
python manage.py runserver
```

Open http://127.0.0.1:8000/ for the store and http://127.0.0.1:8000/admin/ to manage categories and products.

## Usage

| URL                      | What it does                                         |
|--------------------------|------------------------------------------------------|
| `/`                      | Home page with banners and 8 random products         |
| `/category/<id>/`        | Products of one category, with subcategory links     |
| `/add_to_cart/<id>/`     | Adds a product to the session cart, redirects to cart |
| `/cart/`                 | Cart page (template only for now)                    |
| `/checkout/`, `/confirmation/`, `/contact/` | Template pages                    |
| `/admin/`                | Django admin                                         |

## Project structure

```text
shop/
├── manage.py
├── market/              # Django project: settings, root URLs, WSGI/ASGI
├── shop/                # main app
│   ├── models.py        # Category, Subcategory, Product, Order, ...
│   ├── views.py
│   ├── admin.py
│   ├── urls.py
│   └── templates/       # pages and components/ from the Karma template
├── staticfiles/         # template CSS, SCSS, JS and images (STATICFILES_DIRS)
├── media/               # uploaded category and product images
└── db.sqlite3           # sample SQLite database
```

## License

The project code is released under the [MIT License](LICENSE).

The front-end theme is the Karma Shop template by [Colorlib](https://colorlib.com), licensed under CC BY 3.0; keep the Colorlib credit in the footer.
