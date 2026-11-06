# Real Estate Pro - Modern Real Estate Platform & CMS

[![Laravel Version](https://img.shields.io/badge/Laravel-12.x-red.svg?style=flat-square&logo=laravel)](https://laravel.com)
[![PHP Version](https://img.shields.io/badge/PHP-%5E8.2-blue.svg?style=flat-square&logo=php)](https://php.net)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.x-38B2AC.svg?style=flat-square&logo=tailwind-css)](https://tailwindcss.com)
[![Vite](https://img.shields.io/badge/Vite-6.x-646CFF.svg?style=flat-square&logo=vite)](https://vitejs.dev)
[![Leaflet](https://img.shields.io/badge/Leaflet-1.9-green.svg?style=flat-square&logo=leaflet)](https://leafletjs.com)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)

A modern, responsive, and feature-rich Real Estate web application and Content Management System built with **Laravel 12** and **Tailwind CSS**. Designed for real estate agencies, brokers, and property investment firms, this platform provides an intuitive public property portal, interactive map-based discovery, multi-channel lead generation, and an administrative control panel featuring a dynamic theme engine with an in-browser code editor.

---

## Table of Contents

- [Key Features](#-key-features)
  - [Frontend & Public Portal](#frontend--public-portal)
  - [Administrative Control Panel](#administrative-control-panel)
  - [Theme Engine & In-Browser Code Editor](#theme-engine--in-browser-code-editor)
- [Tech Stack](#-tech-stack)
- [Directory Structure](#-directory-structure)
- [Getting Started](#-getting-started)
  - [System Requirements](#system-requirements)
  - [Installation Steps](#installation-steps)
  - [Default Credentials](#default-credentials)
- [Routing Overview](#-routing-overview)
- [Database Schema](#-database-schema)
- [Theme System Guide](#-theme-system-guide)
- [Common Artisan Commands](#-common-artisan-commands)
- [Contributing & License](#-license)

---

## 🌟 Key Features

### Frontend & Public Portal

- **Modern & Responsive UI**: Mobile-first design crafted with Tailwind CSS, supporting smartphones, tablets, and desktop displays.
- **Property Catalog & Filtering**:
  - Filter listings by **Property Type** (Residential, Commercial, Land).
  - Search by **Location / City**.
  - Filter by **Price Range** (Minimum and Maximum budget).
  - Pagination (12 properties per page) for optimized performance.
- **Detailed Property Showcase (`/properties/{id}`)**:
  - Comprehensive property specifications (bedrooms, bathrooms, parking spaces, area in $m^2$).
  - High-resolution photo gallery and responsive image presentation.
  - Agent contact card with direct call and WhatsApp messaging triggers.
  - Granular privacy control (toggle to hide agent information per listing).
  - Smart recommendations for similar properties in the same category or location.
- **Interactive Map Search (`/map`)**:
  - Powered by **Leaflet.js** and **OpenStreetMap**.
  - Interactive property markers with popups displaying thumbnail, title, price, and direct link.
  - Built-in server-side **Geocoding Proxy** (`/geocoding/search`, `/geocoding/reverse`) utilizing Nominatim without client-side CORS issues.
- **Lead Generation & Inquiries**:
  - **General Contact Form (`/contact`)**: Validated customer inquiry submission with automated database storage.
  - **Special Requests Form (`/special-requests`)**: Dedicated form for custom property criteria, target locations, and buyer budgets.
  - **Investor Portal (`/investors`, `/investors/inquiry`)**: Tailored portal for institutional and private investors to submit investment proposals and capital requirements.
  - **Direct Communication**: Instant click-to-chat WhatsApp buttons with pre-populated property information and click-to-call links.

---

### Administrative Control Panel (`/admin`)

- **Secure Authentication**: Built on **Laravel Breeze** with session management, verified emails, and profile editing.
- **Dashboard Overview**:
  - Real-time statistics: total properties, active listings, featured listings, and inquiry counters.
  - Recent activity feeds for contact inquiries and special requests.
- **Property Management (CRUD)**:
  - Create, view, edit, and delete properties.
  - Manage coordinates (latitude and longitude) for map integration.
  - Upload multiple property images with ordering and deletion.
  - Toggle featured properties and listing availability.
  - Filter and search properties by name, property type, and city with instant results.
- **Lead & Inquiry Management**:
  - **Contact Inquiries**: Review submissions, update pipeline status (`new`, `read`, `replied`), and delete processed inquiries.
  - **Special Requests**: Review bespoke property requests and manage status (`pending`, `contacted`, `closed`).
  - **Investment Inquiries**: Manage high-value investment inquiries, budget allocations, and follow-ups.

---

### Theme Engine & In-Browser Code Editor

- **Modular Theme Architecture**: Themes reside in `resources/views/themes/{theme_name}`.
- **One-Click Theme Switching**: Activate themes dynamically from the admin panel without server restarts.
- **Theme Generator**: Create new custom themes with automatic slug generation, copying base templates from the default theme.
- **Built-in Web Code Editor**:
  - Browse theme files and Blade templates in an interactive tree view.
  - Edit template code directly in the browser with full syntax support.
  - Create new template files and delete unused assets without needing SSH or FTP access.

---

## 🛠 Tech Stack

- **Backend Framework**: Laravel 12 (PHP 8.2+)
- **Database & ORM**: MySQL 8+ / MariaDB / SQLite with Eloquent ORM
- **Frontend Framework**: Blade Templating Engine
- **Styling**: Tailwind CSS 3.x, PostCSS, Autoprefixer
- **Build Tool**: Vite 6.x
- **Authentication**: Laravel Breeze
- **Maps & Geolocation**: Leaflet.js, OpenStreetMap, Nominatim Geocoding API (proxied)
- **Icons**: Font Awesome 6.4+

---

## 📁 Directory Structure

```text
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── Admin/                # Admin controllers (Dashboard, Property, Inquiries, Themes)
│   │   │   ├── Auth/                 # Breeze authentication controllers
│   │   │   ├── ContactController.php # Frontend contact inquiries
│   │   │   ├── GeocodingController.php# Server-side Nominatim geocoding proxy
│   │   │   ├── InvestmentController.php# Investor portal inquiries
│   │   │   ├── MapController.php     # Leaflet map endpoint
│   │   │   ├── PageController.php    # Static frontend pages (Home, About, Investors)
│   │   │   ├── ProfileController.php # User profile management
│   │   │   ├── PropertyController.php# Public property catalog & filters
│   │   │   └── SpecialRequestController.php # Custom property requests
│   │   └── Requests/                 # Form request validation classes
│   ├── Models/
│   │   ├── ContactInquiry.php        # Contact inquiry Eloquent model
│   │   ├── InvestmentInquiry.php     # Investment inquiry Eloquent model
│   │   ├── Property.php              # Property listing model with scopes & relations
│   │   ├── PropertyImage.php         # Multi-image relationship model
│   │   ├── SpecialRequest.php        # Special request model
│   │   └── User.php                  # User/Admin authentication model
│   └── Services/
│       └── SettingsService.php       # Dynamic key-value site settings service
├── config/                           # Application configuration files
├── database/
│   ├── migrations/                   # Database schema definitions
│   └── seeders/
│       ├── AdminSeeder.php           # Default admin account seeder
│       ├── DatabaseSeeder.php        # Master seeder
│       └── PropertySeeder.php        # Sample real estate listings
├── resources/
│   ├── css/                          # Tailwind and custom CSS assets
│   ├── js/                           # JavaScript & Vite entry points
│   └── views/
│       ├── admin/                    # Admin panel Blade templates
│       ├── auth/                     # Authentication Blade views (login, register, reset)
│       ├── layouts/                  # Base application layouts
│       └── themes/
│           └── default/              # Default frontend theme (pages, layouts, theme.json)
├── routes/
│   ├── auth.php                      # Authentication route definitions
│   └── web.php                       # Application web routes (frontend, admin, geocoding)
└── storage/                          # Uploaded property images, logs, and framework cache
```

---

## 🚀 Getting Started

### System Requirements

- **PHP**: `^8.2` (Extensions: `bcmath`, `ctype`, `curl`, `dom`, `fileinfo`, `mbstring`, `openssl`, `pdo_mysql`, `tokenizer`, `xml`)
- **Composer**: `^2.0`
- **Node.js**: `^18.0` or `^20.0` & **NPM**: `^9.0`
- **Database**: MySQL 8.0+, MariaDB 10.4+, or SQLite 3.35+

---

### Installation Steps

1. **Clone the repository**:
   ```bash
   git clone <repository-url> realestate
   cd realestate
   ```

2. **Install PHP and Node dependencies**:
   ```bash
   composer install
   npm install
   ```

3. **Configure the environment file**:
   ```bash
   cp .env.example .env
   php artisan key:generate
   ```

4. **Set up database credentials in `.env`**:
   ```env
   DB_CONNECTION=mysql
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=realestate
   DB_USERNAME=your_database_user
   DB_PASSWORD=your_database_password
   ```

5. **Run database migrations and sample seeders**:
   ```bash
   php artisan migrate --seed
   ```
   *This automatically sets up the database schema and populates sample properties and default accounts.*

6. **Create the public storage symlink**:
   ```bash
   php artisan storage:link
   ```

7. **Compile frontend assets**:
   ```bash
   # For production build:
   npm run build

   # Or for local development with Hot Module Replacement (HMR):
   npm run dev
   ```

8. **Start the local development server**:
   ```bash
   php artisan serve
   ```
   Access the website at: **`http://localhost:8000`**

---

### Default Credentials

After running `php artisan db:seed`, you can log in with:

| Role | Email | Password | Access Level |
|---|---|---|---|
| **Administrator** | `admin@realestate.com` | `password123` | Full access to `/admin` panel & settings |
| **Demo User** | `test@example.com` | `password` | Standard user profile access |

---

## 📄 Routing Overview

### Public Routes

| Method | URI | Name | Description |
|---|---|---|---|
| `GET` | `/` | `home` | Homepage with hero, search, featured & latest properties |
| `GET` | `/about` | `about` | About the agency, company values, and team |
| `GET` | `/map` | `map` | Interactive map search using Leaflet & OpenStreetMap |
| `GET` | `/properties` | `properties.index` | Paginated property listings with search & filters |
| `GET` | `/properties/{property}` | `properties.show` | Detailed property information & inquiry form |
| `GET` | `/contact` | `contact.create` | Contact form & office details |
| `POST` | `/contact` | `contact.store` | Submit contact inquiry |
| `GET` | `/special-requests` | `special-requests.create` | Custom property search request form |
| `POST` | `/special-requests` | `special-requests.store` | Submit custom property request |
| `GET` | `/investors` | `investors.index` | Investment opportunities and agency portfolio |
| `GET` | `/investors/inquiry` | `investors.create` | Investor inquiry application |
| `POST` | `/investors/inquiry` | `investors.store` | Submit investor inquiry |
| `GET` | `/geocoding/search` | `geocoding.search` | Proxied location coordinate search (Nominatim) |
| `GET` | `/geocoding/reverse`| `geocoding.reverse`| Proxied reverse coordinate lookup |

### Admin Routes (`/admin` - Protected by `auth` middleware)

| Method | URI | Name | Description |
|---|---|---|---|
| `GET` | `/admin` | `admin.dashboard` | Admin dashboard with analytics & counters |
| `RESOURCE` | `/admin/properties` | `admin.properties.*` | Full CRUD operations for listings |
| `POST` | `/admin/properties/{property}/images` | `admin.properties.images.store` | Upload property images |
| `DELETE` | `/admin/properties/{property}/images/{image}` | `admin.properties.images.destroy` | Delete a property image |
| `GET` | `/admin/inquiries` | `admin.inquiries.index` | List customer contact inquiries |
| `GET` | `/admin/inquiries/{inquiry}` | `admin.inquiries.show` | View inquiry details |
| `PATCH` | `/admin/inquiries/{inquiry}/status` | `admin.inquiries.updateStatus` | Update contact inquiry status |
| `DELETE` | `/admin/inquiries/{inquiry}` | `admin.inquiries.destroy` | Delete contact inquiry |
| `GET` | `/admin/requests` | `admin.requests.index` | List special property requests |
| `PATCH` | `/admin/requests/{request}/status` | `admin.requests.updateStatus` | Update special request status |
| `GET` | `/admin/investments` | `admin.investments.index` | List investor inquiries |
| `PATCH` | `/admin/investments/{inquiry}/status` | `admin.investments.updateStatus` | Update investor inquiry status |
| `GET` | `/admin/themes` | `admin.themes.index` | Theme manager & active theme selector |
| `POST` | `/admin/themes` | `admin.themes.store` | Create a new theme clone |
| `POST` | `/admin/themes/activate` | `admin.themes.activate` | Set active frontend theme |
| `GET` | `/admin/themes/{theme}/edit` | `admin.themes.edit` | In-browser theme code editor |
| `POST` | `/admin/themes/{theme}/files` | `admin.themes.files.store` | Create new theme file |
| `PUT` | `/admin/themes/{theme}/files` | `admin.themes.files.update` | Save edited theme file |
| `DELETE` | `/admin/themes/{theme}/files` | `admin.themes.files.destroy` | Delete theme file |

---

## 💾 Database Schema

The database consists of structured relational tables with indexed lookups:

1. **`properties`**:
   - `id`, `title`, `description`, `price`, `type` (`residential`, `commercial`, `land`).
   - `location`, `address`, `latitude`, `longitude`, `area`, `bedrooms`, `bathrooms`, `parking_spaces`.
   - `is_featured`, `is_available`, `hide_agent_info`.
   - `agent_name`, `agent_contact`, `timestamps`.
2. **`property_images`**:
   - `id`, `property_id` (foreign key with cascade delete), `image_path`, `alt_text`, `order`, `timestamps`.
3. **`contact_inquiries`**:
   - `id`, `name`, `email`, `phone`, `subject`, `message`, `status` (`new`, `read`, `replied`), `timestamps`.
4. **`special_requests`**:
   - `id`, `name`, `email`, `phone`, `property_type_preference`, `location_preference`, `budget_range`, `request_details`, `status` (`pending`, `contacted`, `closed`), `timestamps`.
5. **`investment_inquiries`**:
   - `id`, `company_name`, `contact_person`, `email`, `phone`, `investment_type`, `investment_amount`, `preferred_location`, `inquiry_details`, `status`, `timestamps`.
6. **`users`**:
   - Laravel authentication table for administrators and users.
7. **`settings`**:
   - Key-value dynamic configuration table storing runtime options like active theme (`active_theme`).

---

## 🎨 Theme System Guide

### Structure of a Theme

Each theme resides in `resources/views/themes/{theme_folder}/` and includes:

```text
themes/default/
├── theme.json               # Theme metadata (name, description, version, author, screenshot)
├── layouts/
│   └── app.blade.php        # Master layout (HTML head, navbar, footer)
├── home.blade.php           # Homepage template
├── about.blade.php          # About Us page
├── map.blade.php            # Map discovery page
├── contact/                 # Contact page templates
├── properties/              # Properties index and show views
├── special-requests/        # Special request form views
└── investors/               # Investor portal views
```

### `theme.json` Specification

```json
{
    "name": "Luxury Estate",
    "description": "Modern minimalist dark theme with gold accents.",
    "version": "1.0.0",
    "author": "Your Agency",
    "screenshot": "https://example.com/screenshot.jpg"
}
```

Themes can be customized without editing core controllers. The `SettingsService` resolves the active theme view dynamically at runtime.

---

## ⚡ Common Artisan Commands

| Task | Command |
|---|---|
| Start local server | `php artisan serve` |
| Run migrations | `php artisan migrate` |
| Reset & re-seed database | `php artisan migrate:refresh --seed` |
| Clear all caches | `php artisan optimize:clear` |
| Cache routes & config | `php artisan optimize` |
| List registered routes | `php artisan route:list` |
| Link storage directory | `php artisan storage:link` |
| Open interactive shell | `php artisan tinker` |
| Run test suite | `php artisan test` |

---

## 🔒 Security & Best Practices

- **CSRF Protection**: All POST/PUT/PATCH/DELETE forms are secured with Laravel CSRF tokens.
- **SQL Injection Prevention**: Eloquent ORM parameterized queries prevent SQL injection across all models.
- **XSS Sanitization**: Blade syntax (`{{ $var }}`) automatically escapes unsafe user content.
- **Input Validation**: Dedicated form requests and validation rules ensure clean input before processing.
- **CORS Protection**: Nominatim geocoding requests are proxied via server-side controller, safeguarding API endpoints.

---

## 📄 License

This application is open-source software licensed under the [MIT license](https://opensource.org/licenses/MIT).
