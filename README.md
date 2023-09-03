## laravel tips & tricks

A new small improvement in the latest Laravel 10.11.<br>
You can now call dd() or dump() for Carbon objects, useful at the end of chaining, <br>for example.

- Instead of (previous version):<br>
```php
$var= now()->addDays(7);
dd($var);
```
- From Laravel 10.11:<br>
```php
now()->addDays(7)->dd();
```
<br>

# before and after validation rules in Laravel.

You can use the before and after validation rules in Laravel. <br>
It’s very useful if you’re working with dates that depend on each other: <br>for example.

```php
class ProductRequest extends FromRequest
{
	public function rules():array
		return[
			'publishAt' =>[
				'required',
				'date',
				'before:publishAt'
			],
			'archiveAt'=>[
				'required',
				'date',
				'after:publishAt'
			]
		]
	}
}
```
# Different type of 'if condition'.

You can choose the best option of 'if condition'. <br>
<br>for example.

```php
public function hasLimitations(Account $account):bool
	if($account->has_access_to_paid_version_for_sale){
		return false;
	}
	if(! config('app.requires_subscription')){
		return false;
	}
	if($account->isSubscribed()){
		return false;
	}
	return true;
}

public function hasLimitations(Account $account):bool
	if($account->has_access_to_paid_version_for_sale){ || (! config('app.requires_subscription')) || ($account->isSubscribed()) {
		return false;
	}
	return true;
}

public function hasLimitations(Account $account):bool
	return (($account->has_access_to_paid_version_for_sale) && (! config('app.requires_subscription')) && ($account->isSubscribed())));
```
# 'iseet' accepts more than one parameter.
Did you know that isset() accepts more than one parameter?<br>
<br>for example.
- Instead of doing this:<br>
```php
if(isset($book) && isset($pen)){

}
```
- Now you can do this<br>
```php
if(isset($book,$pen)){

}
```
# Multiple parameter in 'OrWhere'.
You can pass multiple parameters to "orWhere"<br>
<br>for example.
- Normal way:<br>
```php
$user->whare('name','asif');
$user->orWhare('age',28);
$user->orWhare('city','Rangpur');
```
- Smart way<br>
```php
$user->whare('name','asif');
$user->orWhare(['age'=>28,'city'=>'Rangpur']);
```
# Eloquent Model name differs from the table name?.
Eloquent Model name differs from the table name?<br> No problem, you can specify the table name in the protected property called "table" of Eloquent Model.<br>
<br>for example.
```php
class UserDetails extends Model
{
	protected $table='addresses'
}
```
# Laravel Eloquent.
Tips of laravel eluquent
- Eager loading relationships with "with"
```php
$user=User::with('posts')->get();
```
- Filtering basen on related records existance using "has"
```php
$activeUser=User::has("posts")->get();
```
- Combining "with" and "whereHas" with "withWhereHas"
```php
$userWithActive=User::withWhereHas('posts',function($qs){
	$qs->where('active',true);
}
)->get();
```
- Nested relationship contains with "whereRelations"
```php
$userWithRelation=User::whereRelation('posts.comments','active',true)->get();
```
- Maching any related record using "orWhere"
```php
$userMachingRecord=User::whereHas('posts',function($qs){
	$qs->where('active',true);
})->orWhereHas('comments',function($qs){
	$qs->where('active',true);
})->get();
```
- Models without related records using "deosntHave"
```php
$result=User::deosntHave('posts')->get();
```
- Models without specific relationship conditions using "whereDeosntHave"
```php
$result=User::whereDeosntHave('comments',function($qs){
	$qs->where('active',false);
})->get();
```
- Reletions sum "withSum"
```php
$result=User::withSum('comments','likes')->get();
```
- Check if related record exists using "withExists"
```php
$result=User::withExists('posts')->where('active',true)->get();
```
- Retrieve relationship count using  "withCounts"
```php
$result=User::withCounts('posts')->where('active',true)->get();
```
