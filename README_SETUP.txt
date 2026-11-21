DRIVECARE - MYSQL + PHP BACKEND STARTER
======================================

WHAT THIS PACKAGE CONTAINS
- database.sql: creates the complete MySQL schema.
- api/config.php: database and allowed Netlify origin settings.
- api/index.php: PHP JSON API (register/login/logout and CRUD).
- frontend/drivecare-api.js: JavaScript helper for your Netlify frontend.

IMPORTANT HOSTING FACT
Your Netlify URL serves the frontend. Netlify does not execute PHP scripts or host a MySQL server.
Deploy the /api folder to a PHP-capable host and create MySQL there. Keep the frontend on Netlify.
Official Netlify explanation: https://answers.netlify.com/t/support-guide-can-i-run-a-web-server-http-listener-and-or-database-at-netlify/3078

STEP 1 - CREATE MYSQL DATABASE
1. Open phpMyAdmin from your PHP hosting control panel (or local XAMPP phpMyAdmin).
2. Import database.sql.
3. Confirm database drivecare_db and its tables have been created.
4. Create a dedicated database user with access only to drivecare_db.

STEP 2 - DEPLOY PHP API
1. Upload the api folder contents to a PHP 8+ hosting account, for example:
   public_html/api/index.php
   public_html/api/config.php
2. In config.php, set db_host, db_name, db_user and db_pass to the values from your host.
3. Set allowed_origin exactly to:
   https://tranquil-stroopwafel-79ce6a.netlify.app
4. Enable HTTPS/SSL on the PHP host.
5. Test by opening:
   https://YOUR-PHP-HOST.example.com/api/index.php?resource=vehicles
   It should return a JSON authentication error (401), not a PHP error.

STEP 3 - CONNECT NETLIFY FRONTEND
1. Copy frontend/drivecare-api.js into your website project.
2. Change API_BASE to your real PHP API URL.
3. Include it in the HTML after your existing page scripts or before the script that uses it:
   <script src="/drivecare-api.js"></script>
4. Replace demo login logic with:
   const user = await drivecareLogin(email, password);
5. Replace demo data reads with:
   const vehicles = await drivecareList("vehicles");
   const reminders = await drivecareList("reminders");
   const services = await drivecareList("services");
   const expenses = await drivecareList("expenses");
   const fuel = await drivecareList("fuel");
6. Use drivecareCreate(resource, object) to save forms, drivecareUpdate(resource,id,object)
   to edit, and drivecareDelete(resource,id) to delete.
7. Redeploy the updated frontend to the SAME Netlify site.

EXAMPLE VEHICLE INSERT
await drivecareCreate("vehicles", {
  make: "Toyota",
  model: "Innova",
  year: 2022,
  registration_number: "KA01AB1234",
  fuel_type: "Diesel",
  odometer_km: 25000
});

AVAILABLE API RESOURCES
GET/POST: vehicles, reminders, services, fuel, expenses, notifications
GET/PATCH/DELETE: same resources (PATCH and DELETE require ?id=123)
POST: register, login, logout
GET: me

SECURITY NOTES
- Use HTTPS only.
- Do not put MySQL credentials in frontend JavaScript or Netlify files.
- Do not commit config.php with real credentials to a public GitHub repository.
- Change the example database credentials immediately.
- This starter uses password_hash/password_verify, prepared SQL statements, random bearer tokens,
  token hashes in the database, and per-user row filtering.
- For production use, add rate limiting, CSRF protections where relevant, audit logging,
  backups, and stricter input validation. Set appropriate upload/file permissions.
- The PHP API is a starter integration and has not been deployed or tested against your hosting account.

LOCAL TESTING WITH XAMPP
1. Install XAMPP and start Apache + MySQL.
2. Put api folder in htdocs/drivecare/api.
3. Import database.sql in http://localhost/phpmyadmin.
4. Set config.php DB settings to localhost / drivecare_db / root / (blank password if that is
   your local XAMPP default).
5. For local frontend testing, serve your Netlify files from a local web server and temporarily
   set allowed_origin to that exact local origin (for example http://localhost:5500).
6. Set API_BASE in drivecare-api.js to:
   http://localhost/drivecare/api/index.php
