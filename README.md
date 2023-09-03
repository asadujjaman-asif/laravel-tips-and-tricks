## laravel tips & tricks

A new small improvement in the latest Laravel 10.11.
You can now call dd() or dump() for Carbon objects, useful at the end of chaining, for example.

- Instead of (previous version):
- **[$var= now()->addDays(7);]
dd($var);
- From Laravel 10.11:
now()->addDays(7)->dd();