django-requestlogger
====================

This very application, `django-requestlogger`, is a pluggable (plug'n'play!) solution for logging, monitoring and analyzing data about all requests (and responses) to your django powered website. Depending on log verbosity mode, it can save response times, capture all "logging" (default Python module) output and SQL queries, show you peak, average and sample data and, if needed, log complete request and response information, both meta and content. The main idea is that you just install it, and the data starts collecting instantly, providing you with a lot of useful information.

All the data is collected to the database, so be careful with verbosity level. If it becomes an issue, you can use auto-cleanup, log only some of requests (like 10% of them) or restrict logging only to slow or failing requests.

## Installation

Just install the module

    pip install django-requestlogger

Add `requestlogger` to the `INSTALLED_APPS` settings and add `requestlogger.middleware.RequestLoggingMiddleware` to `MIDDLEWARE_CLASSES`. Then run `python manage.py syncdb` and, if you use `south`, `python manage.py migrate`.

To see the gathered statistics, you'll need the `django.contrib.admin` installed (you probably have already had it).

Try opening a few pages on the website. Then open 'Requestlogger / Requests' in the Admin, and see what data is available by default.

## Configuration

As you can see, `django-requestlogger` works out of the box, but you'll probably want to play with settings.

`REQUEST_LOGGING_MODE` is a string with one of these values:

* `all` (default) logs all requests to your database. Be careful to use it in production, since it can probably overwhelm your database. It does one `INSERT` query per request
* `off` logs nothing, it's useful if you want to switch it off quickly
* `paranoid` mode

`REQUEST_LOGGING_EXCLUDE_URLS` is a list of regular expressions (`['^/admin/', '^/favicon.ico']` by default). All requests to urls that match at least one of these won't be logged. Please note that, unlike the urlconf, there is a slash in the beginning of each path, so you should start your path with `^/` (if match from the beginning is needed).

`REQUEST_LOGGING_EXCLUDE_VIEWS` is another list of regexps, but they are tested on the view name (with a module, like `django.views.generic.View`).

Each one of these settings can be changed in runtime without restarting the django application.

# Screenshots

![Views](http://f.cl.ly/items/2t0k1a110b3e2u2e0h33/Screen%20shot%202011-06-27%20at%207.25.08%20PM.png)
![Requests](http://f.cl.ly/items/2V3m3c3e3Y1L3E331m1i/Screen%20shot%202011-06-27%20at%207.26.33%20PM.png)

# Security implications

# Performance implications

# Storage backends

# Extending with your own parameters