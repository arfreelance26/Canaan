# Canaan Global International — Corporate Website

A modern, high-performance logistics and freight forwarding corporate website built with Next.js. Engineered for exceptional SEO, interactive 3D visualizations, and robust security, tailored specifically for static deployment on GoDaddy cPanel.

## Tech Stack

- **Framework**: Next.js 16 (App Router)
- **UI & Styling**: Tailwind CSS, Lucide React
- **3D Visualization**: Three.js, React-Globe.gl
- **Contact Form**: EmailJS (Serverless email routing)
- **Deployment Strategy**: Static HTML Export (Apache/cPanel)

---

## Architecture & Features

### 1. Static Export Optimization
The application is configured specifically for traditional shared hosting (like GoDaddy cPanel) where a Node.js runtime is unavailable.
- `next.config.mjs` enforces `output: 'export'`.
- Next.js Image Optimization is bypassed (`unoptimized: true`) to ensure images compile perfectly to static HTML.
- All static assets (images, logos) are served directly from the `public/` directory via absolute string paths.

### 2. Search Engine Optimization (SEO)
Built from the ground up to rank for logistics keywords globally and regionally (Tuticorin, India).
- **JSON-LD Schema**: Included in the root `layout.js` to provide Google with structured business data.
- **Dynamic Metadata**: Dedicated `layout.js` files for `/about`, `/cargo`, and `/canaan-shipping-services` ensure granular, keyword-rich titles and descriptions.
- **Crawling**: Auto-generated `sitemap.xml` and `robots.txt` utilizing Next.js 13+ App Router conventions (`force-static`).

### 3. Security
Security is handled at the server level via an Apache `.htaccess` file located in the `public/` directory (which compiles into the `/out` root).
- **CSP (Content-Security-Policy)**: Restricts script execution to trusted domains (EmailJS, Google Maps).
- **HSTS (Strict-Transport-Security)**: Enforces HTTPS.
- **X-Frame-Options**: Prevents clickjacking.

---

## Local Development

### Prerequisites
- Node.js 18.17 or later
- npm, yarn, pnpm, or bun

### 1. Environment Variables
To enable the Contact Form functionality, create a `.env.local` file in the root directory and add your EmailJS credentials:

```env
NEXT_PUBLIC_EMAILJS_SERVICE_ID=your_service_id
NEXT_PUBLIC_EMAILJS_TEMPLATE_ID=your_template_id
NEXT_PUBLIC_EMAILJS_PUBLIC_KEY=your_public_key
```

### 2. Run the Development Server
Install dependencies and spin up the local server:

```bash
npm install
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) to view the application.

---

## Deployment (GoDaddy cPanel)

Deploying to cPanel requires generating a static build. Follow these steps:

1. **Build the Project**
   ```bash
   npm run build
   ```
   *This command tells Next.js to generate static HTML/CSS/JS files into an `/out` directory.*

2. **Upload to cPanel**
   - Compress the contents of the newly generated `/out` folder into a `.zip` file.
   - Log in to your GoDaddy cPanel and open the **File Manager**.
   - Navigate to your `public_html` directory (or the root directory of your add-on domain).
   - Upload the `.zip` file and extract its contents directly into the directory.

> **Note:** The `public/.htaccess` file is automatically copied into the `/out` directory during the build. Ensure that hidden files (dotfiles) are visible in your FTP client/cPanel File Manager to verify its transfer.

---

## Project Structure

```text
├── app/
│   ├── about/                   # About page & SEO layout
│   ├── canaan-shipping-services/# Services page & SEO layout
│   ├── cargo/                   # Cargo gallery & SEO layout
│   ├── components/              # Reusable UI (Navbar, Contact, Globe, Timeline)
│   ├── layout.js                # Root layout (JSON-LD, Global Metadata)
│   ├── page.js                  # Landing page
│   ├── sitemap.js               # Auto-generates sitemap.xml
│   └── robots.js                # Auto-generates robots.txt
├── public/
│   ├── company_photos/          # Static images & assets
│   └── .htaccess                # Apache security & caching headers
├── next.config.mjs              # Next.js export & image config
└── package.json                 # Dependencies & Build scripts
```
