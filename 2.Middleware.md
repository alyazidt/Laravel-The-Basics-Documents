# Laravel-The-Basics-Documents : Middleware

## Introduction : 
Middleware provide a convenient mechanism for inspecting and filtering HTTP requests entering your application.

Think of middleware as a security guard standing at the entrance of your Laravel application.

Every request (like opening a page or submitting a form) must pass through this guard before it reaches the core part of your app.

This guard (middleware) can:

✅ Allow the request to continue

❌ Block the request

🔁 Redirect the request to another page (like the login page)

---
Simple Example:

Let’s say you have a Dashboard page that should only be opened by logged-in users.

If someone is not logged in and tries to open the dashboard:

→ Middleware says: “Stop! You need to log in first”

→ And redirects them to the Login page.


If someone is already logged in:

→ Middleware says: “You’re good to go!”

→ And lets the request continue to the Dashboard.

---
Laravel comes with several built-in middleware, including:

auth – for checking if the user is logged in

csrf – for protecting forms from cross-site request forgery

---
All (user-defined) middleware are usually placed in:

app/Http/Middleware
#

# Defining Middleware :

To create a new middleware in Laravel, use the following command:

`php artisan make:middleware EnsureTokenIsValid`

This will create a file named EnsureTokenIsValid.php in the app/Http/Middleware directory.

Here’s a simple example where we check if a request has a valid token:

` <?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;

class EnsureTokenIsValid
{
    public function handle(Request $request, Closure $next): Response
    {
        if ($request->input('token') !== 'my-secret-token') {
            return redirect('/home');
        }

        return $next($request);
    }
}
`






