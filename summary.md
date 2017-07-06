# Code Smart - Summary (For me)
==================================================================================================

# install laravel

composer create-project laravel/laravel example

# lifecycle of a single request to a Laravel framework application

Laravel uses a front-controller and router combination. What this means is that there's only a single PHP file in your web root directory, and all requests to your application will be made through this script. This file is called index.php and you'll find it in the public directory, which is the only directory that should be accessible on the web.

Request > Services > Routing > Logic > Response

# Request

Using Laravel, the information for the current request is stored in an instance of the class Illuminate\Http\Request, which extends from the Symfony Framework Symfony\Component\HttpFoundation\Request class.

# Services

See services.md

# Routing

See routing.md

# Logic

It's where you'll be talking to a database, validating forms, or showing pages.

See logic.md

# Response

The response is created at the end of your logic. It might be a HTML template. It might be some JSON data; it might just be a string. Hey, it might be nothing at all. In some sad circumstances, it might be an error screen or a 404 page!

Summary: The web browser sends a request. Laravel bootstraps its services, interrogates the request, and performs routing operations. Our code is executed and delivers a response to the user.
