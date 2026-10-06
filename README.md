# Flybees — Full-Stack E-commerce Application

Flybees is a server-rendered e-commerce project with customer shopping flows and an administration area. It brings together an Express backend, EJS pages, MongoDB persistence, and payment integration.

## Technology stack

| Layer | Technologies |
| --- | --- |
| Web interface | EJS templates, CSS, browser JavaScript |
| Server | Node.js, Express |
| Database | MongoDB, Mongoose |
| Sessions and passwords | express-session, bcrypt |
| Integrations | Razorpay, Nodemailer |
| Uploads and reports | Multer, PDFKit, ExcelJS, XLSX |

## Application areas

The repository includes routes and controllers for:

- Customer registration, login, OTP-related flows, and password recovery.
- Product browsing, search, category filtering, cart quantities, and checkout.
- Customer addresses, orders, cancellation, and wallet flows.
- Razorpay order creation and payment verification.
- Admin product, category, banner, coupon, customer, and order management.
- Dashboard data and sales reporting.

These describe the code present in the repository; end-to-end behavior still needs verification in a configured local environment.

## Architecture

Express mounts customer routes at `/` and administrative routes at `/admin`. Route handlers delegate to controllers, which use Mongoose models and render EJS views.

| Path | Responsibility |
| --- | --- |
| `server.js` | Express startup, sessions, view configuration, route mounting |
| `routes/` | Customer and admin endpoints |
| `controllers/User/` | Shopping and customer account workflows |
| `controllers/Admin/` | Catalog administration, order management, reporting |
| `model/` | Mongoose data models |
| `database/connection.js` | MongoDB connection |
| `middleware/` | Authentication-related middleware, uploads, error handling |
| `views/` | Customer and admin EJS pages |
| `public/` | Static assets |
| `utils/` | Shared utilities |

## Local setup

Prerequisites: Node.js with npm, a MongoDB instance, and Razorpay test credentials for payment-related initialization and testing. The project does not currently declare a supported Node.js version.

1. Clone and install dependencies:

   ```bash
   git clone https://github.com/mithrafaris/flybees-ecommerce.git
   cd flybees-ecommerce
   npm ci
   ```

2. Create a local `.env` file:

   ```dotenv
   PORT=8080
   MONGO_URL=mongodb://127.0.0.1:27017/flybees
   RAZORPAY_ID_KEY=your_test_key_id
   RAZORPAY_SECRET_KEY=your_test_key_secret
   ```

   Use your own test credentials and keep the environment file out of version control.

3. Start the application:

   ```bash
   npm start
   ```

4. Open [the local storefront](http://localhost:8080). The admin login route is `/admin/Adminlogin`; an existing admin account is required.

Email recovery currently has configuration embedded in its controller and a localhost reset URL. Move email credentials into environment variables and configure the correct application URL before testing that flow. The environment variables above alone do not configure email delivery.

## Verification and follow-up work

The current `npm test` script is a placeholder and exits with an error. Local setup and application flows have not been execution-tested as part of this documentation update.

Before treating the application as deployment-ready:

- Review authorization on every admin and customer-specific endpoint.
- Replace the hardcoded session secret and review session storage and cookie options.
- Move embedded email credentials out of source; rotate any real credentials that were committed.
- Verify payment signatures, order totals, inventory changes, cancellations, and wallet behavior end to end.
- Add meaningful tests for authentication, authorization, and checkout.
- Add verified screenshots and a working demo link after deployment validation.

## Full-stack discussion points

This project provides code to discuss server-rendered UI, Express routing, database modeling, shopping workflows, third-party integrations, and the separation of customer and admin functionality.
