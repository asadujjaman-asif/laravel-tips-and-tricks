## laravel tips & tricks

A new small improvement in the latest Laravel 10.11.<br>
You can now call dd() or dump() for Carbon objects, useful at the end of chaining, <br>for example.

- Instead of (previous version):<br>
`$var= now()->addDays(7);`<br>
`dd($var);`<br>
- From Laravel 10.11:<br>
`now()->addDays(7)->dd();`<br>

# before and after validation rules in Laravel.

You can use the before and after validation rules in Laravel. <br>
It’s very useful if you’re working with dates that depend on each other: <br>for example.

`class ProductRequest extends FromRequest`<br>
&nbsp;`{`<br>
&ensp;`public function rules():array`<br>
&ensp;&nbsp;`return [`<br>
&emsp;&nbsp;`'publishAt' =>[`<br>
&emsp;&ensp;`'required',`<br>
&emsp;&ensp;`'date',`<br>
&emsp;&ensp;`'before:publishAt'`<br>
&ensp;&nbsp;`],`<br>
&emsp;&nbsp;`'archiveAt'=>[`<br>
&emsp;&ensp;`'required',`<br>
&emsp;&ensp;`'date',`<br>
&emsp;&ensp;`'after:publishAt'`<br>
&ensp;&nbsp;`]`<br>
&ensp;`];`<br>
&ensp;`}`<br>
&nbsp;`}`<br>

# Deferent option of if conditons.

You can use the best option of if as your like. <br>
<br>for example.

`class ProductRequest extends FromRequest`<br>
`{`<br>
`public function rules():array`<br>
`return [`<br>
`'publishAt' =>[`<br>
`'required',`<br>
`'date',`<br>
`'before:publishAt'`<br>
`],`<br>
`'archiveAt'=>[`<br>
`'required',`<br>
`'date',`<br>
`'after:publishAt'`<br>
`]`<br>
`];`<br>
`}`<br>
`}`<br>