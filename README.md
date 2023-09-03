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

`public function hasLimitations(Account $account):bool`<br>
&nbsp;`if($account->has_access_to_paid_version_for_sale){`<br>
&ensp;`return false`<br>
&nbsp;`}`<br>
&nbsp;`'if(! config('app.requires_subscription')){`<br>
&ensp;`return false;`<br>
&nbsp;`}`<br>
&nbsp;`'if($account->isSubscribed()){`<br>
&ensp;`return false;`<br>
&nbsp;`}`<br>
&nbsp;`return true;`<br>
`}`<br>
<br>

`public function hasLimitations(Account $account):bool`<br>
&nbsp;`if($account->has_access_to_paid_version_for_sale){ || (! config('app.requires_subscription')) || ($account->isSubscribed()) {`<br>
&ensp;`return false`<br>
&nbsp;`}`<br>
&nbsp;`return true;`<br>
`}`<br>

<br>

`public function hasLimitations(Account $account):bool`<br>
&nbsp;`return (($account->has_access_to_paid_version_for_sale) && (! config('app.requires_subscription')) && ($account->isSubscribed())))`<br>