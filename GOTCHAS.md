# 🚨 The "Gotchas" Guide: Hidden Traps in CI4 Migration

You've updated your syntax, but your app is still acting weird? You've likely hit one of these hidden architectural changes between CodeIgniter 3 and CodeIgniter 4. 

---

## Gotcha 1: The "White Screen of Death" (Public Folder)
**The Problem:** After migrating, you navigate to your site and get a 404, a 500 error, or a blank white screen.
**Why it happens:** In CI3, your `index.php` was in the root directory. In CI4, **all web traffic MUST go through the `public/` directory** for security reasons. Your old `.htaccess` rules are now broken.
**The Fix:** 
1. Update your web server (Apache/Nginx) document root to point to `/your-project/public`.
2. If you are using a local `.htaccess` in the root for development, copy the default `public/.htaccess` provided by CI4 and ensure `RewriteBase` is correct.

---

## Gotcha 2: "Class 'Config\App' not found" or Autoloading Failures
**The Problem:** Your custom libraries or helpers suddenly can't be found, even though the files are there.
**Why it happens:** CI3 used `application/config/autoload.php`. CI4 uses PSR-4 namespacing and a completely different autoloader (`app/Config/Autoload.php`).
**The Fix:** 
1. Ensure every new class you create has the correct namespace at the top (e.g., `namespace App\Libraries;`).
2. If you have custom folders outside `app/`, you must register them in `app/Config/Autoload.php` under the `$psr4` array.
3. Run `composer dump-autoload` in your terminal if you added new namespaces.

---

## Gotcha 3: Database Config is Ignored
**The Problem:** You updated `app/Config/Database.php`, but the app is still trying to connect to the old CI3 database, or it throws a connection error.
**Why it happens:** CI4 heavily prioritizes the `.env` file over the PHP config files. If a `.env` file exists, it overrides `app/Config/Database.php`.
**The Fix:** 
1. Check if you have a `.env` file in your root directory (copy `.env.example` to `.env` if you don't).
2. Uncomment and update the database lines in the `.env` file:
    env
    database.default.hostname = localhost
    database.default.database = your_ci4_db
    database.default.username = root
    database.default.password = yourpassword
    database.default.DBDriver = MySQLi


---

## Gotcha 4: Session Data Disappears Between Requests
**The Problem:** You log a user in, but on the next page load, `session()->get('user_id')` returns null.
**Why it happens:** CI4 has stricter security defaults for cookies, including `session.cookie_samesite = Lax` (or Strict), and the session save path might not be writable.
**The Fix:**
1. Ensure the `writable/session` directory exists and has proper write permissions (`chmod 777` or `chown` depending on your server).
2. Check `app/Config/App.php` and ensure `$sessionSavePath` is correctly pointing to a valid, writable directory (or use the database driver).
3. If testing locally on `http://` (not `https://`), ensure `$cookieSecure` is set to `false` in `app/Config/App.php`.

---

## Gotcha 5: Helper Functions "Do Not Exist"
**The Problem:** You try to use `base_url()` or `form_open()` and get a "Call to undefined function" error.
**Why it happens:** In CI3, you loaded helpers via `$this->load->helper('url')`. In CI4, helpers are global functions, but they still need to be loaded *once* per request, usually in the BaseController or via the `$globals` array in `app/Config/Autoload.php`.
**The Fix:**
Open `app/Config/Autoload.php` and add the helpers you need to the `$helpers` array so they load automatically on every request:
```php
public $helpers = ['url', 'form', 'html', 'security'];




