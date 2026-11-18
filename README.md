# Pharmacy Cashier System (Apotek)

A cashier web app for a pharmacy, built with Laravel. Staff manage the medicine catalog, create customer orders, and print or download receipts.

## Features

- **Role-based access** with three roles (`admin`, `kasir`, `user`), enforced by a custom `cekRole` middleware
- **Medicine management:** type (tablet, syrup, capsule), name, photo, price, and stock
- **Order creation:** select medicines, quantities are grouped automatically, and subtotal and total are calculated
- **Receipts:** printable receipt page and PDF download (DomPDF)
- **User management** for admins
- Orders store their line items as JSON, so a receipt keeps the price at the time of purchase

## Roles

| Role | Access |
|---|---|
| `admin` | User management, medicines, orders, dashboard |
| `kasir` | Medicines, orders, receipts, dashboard |
| `user` | Home page |

## Tech stack

- PHP 8.1, Laravel 10
- MySQL
- Blade templates
- `barryvdh/laravel-dompdf` for PDF receipts
- `maatwebsite/excel` (an orders export class is included)

## Getting started

Requirements: PHP 8.1+, Composer, MySQL.

```bash
git clone https://github.com/Hidayatmramon/pharmacy-cashier-system.git
cd pharmacy-cashier-system
composer install
cp .env.example .env
php artisan key:generate
```

Create an empty database, then set `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD` in `.env`.

```bash
php artisan migrate --seed
php artisan storage:link
php artisan serve
```

The seeders create sample medicines and accounts for each role. Their credentials are defined in `database/seeders/UserSeeder.php`. They are meant for local development only.

## Roadmap

- Reduce medicine stock when an order is created, and block orders that exceed stock
- Make the tax rate configurable instead of fixed in `OrderController`
- Validate uploaded photos (image type and size)
- Wrap order creation in a database transaction
- Use `POST` for logout instead of `GET`
- Route the existing Excel export for orders

## Status

Learning project, not actively developed.
