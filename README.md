## laravel tips & tricks

A new small improvement in the latest Laravel 10.11.<br>
You can now call dd() or dump() for Carbon objects, useful at the end of chaining, <br>for example.

- Instead of (previous version):<br>
$var= now()->addDays(7);<br>
dd($var);<br>
- From Laravel 10.11:<br>
![#dddddd]now()->addDays(7)->dd();<br>`#dddddd`