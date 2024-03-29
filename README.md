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
## Laravel request rule
You can implement password validations in Laravel using the Password rule object. 
Easily customize complexity requirements with methods like.
- min()
- letters()
- mixedCase()
- numbers()
- symbols()
- uncompromised()
```php
use Illuminate\Support\Facades\Validator;
use Illuminate\Validator\Rules\Password;
//Create  a validator instance
$validator = Validator::make($request->all(),[
	'password'=>[
		'required', //Password is required
		'confirmed', // Password Must be confirmed
		Password::min(8) //Password should be minimum 8 characters length
		->letters() // Password should containt at least 1 latter
		->mixedCase() //Password should containt at least 1 uppercase latter and 1 lowercase latter
		->numbers() // Password should containt at least 1 number
		->uncompromised(); /// Password should not be compromised in a data leak
	],
]);
$validator->fails()? 'Validation errors': 'validations passed';
```
## Laravel relation
Boost performance and efficiency with these 10 amazing tips using the 'with()' method. Level up your relationships game!
- Load multiple relationships
```php
$user = User::with(['posts','comments'])->find();
```
- Load nested relationships
```php
$posts = Post::with('comments.user')->get();
```
- Load relationships with constraints
```php
$user = User::with(['posts',($qs)=>{
	$qs->where('published',true);
}])->find(1);
```
- Load relationships with custom select collumns
```php
$user = User::with(['posts',($qs)=>{
	$qs->select('published','title');
}])->get();
```
- Load relationships with pagination
```php
$user = User::with(['posts',($qs)=>{
	$qs->select('created_at','asc')->paginate(20);
}])->get();
```
- Load relationships with specific columns
```php
$user = User::with('post:title,description')->find(1);
```
- Load relationships with random related models
```php
$user = User::with(['posts',($qs)=>{
	$qs->inRandomOrder()->limit(20);
}])->get();
```
- Load relationships with custom aliases
```php
$user = User::with(['latesDate as currentDate',($qs)=>{
	$qs->latest()->limit(20);
}])->get();
```
- Load relationships with custom aliases
```php
$user = User::with(['latesDate as currentDate',($qs)=>{
	$qs->latest()->limit(20);
}])->get();
```
- Load relationships conditionally
```php
$user = User::with(['latesDate as currentDate',($qs)=>{
	$qs->with('secretId')->limit(20);
}])->get();
```
- Load relationships based on a methods return value
```php
$user = User::with(User::resolvRelationships())->get();
```
## Laravel dump() & dd()
Laravel request class has been added dd & dump.
- dump & die all request datas
```php
$request->dd();
```
- dump and die specific keys
```php
$request->dd('name');
$request->dd(['name','address']);
```
- dump all request datas
```php
$request->dump();
```
- dump specific keys
```php
$request->dump('name');
$request->dump(['name','address']);
```
- You can use also request helper
```php
$request()-?dd();
$request()-?dump();
```
## toArray & attributesToArray 
Developers! Use toArray & attributesToArray for streamlined data handling.
- dump & die all request datas
```php
$user=User::with('posts')->find(1);
```
- Use toArray method and get result of their post.
```php
$result = $user->toArray();
```
- Oupput of the users
```php
[
	'name'=>'Jhon'
	'age'=>65,
	'created_at'=>'2023-07-28:12-55-36',
	'updated_at'=>'2023-07-28:12-55-36',
	'post'=>[
		//this is post list
	]
]
```
- Use attributesToArray method and get result of their post.
```php
$result = $user->attributesToArray();
```
- Oupput of the user
```php
[
	'name'=>'Jhon'
	'age'=>65,
	'created_at'=>'2023-07-28:12-55-36',
	'updated_at'=>'2023-07-28:12-55-36'
]
```
## Laravel latest() & oldest() 
 If you need to order a query, you can use the latest() and oldest() methods, making everything a bit nicer within your codebase.
- Traditional way of ordering 'latest' data
```php
$user=User::orderBy('id','desc')->get();
```
- Smart Way.
```php
$user=User::latest()->get();
```
- Traditionals way of ordering 'oldest' data
```php
	$user=User::orderBy('id','asc')->get();
```
- Smart way.
```php
$user=User::oldest(')->get();
```
## isset vs data_get() in php
  data_get() is really useful when it comes to dealing with arrays and accessing keys. Which do you prefer? 
```php
$data=[
    'products'=>[
        'item'=>[
            'name'=>'HP Laptop',
            'price'=>70000
        ]
    ]
];
```
- Get ammount.
```php
$price=isset($data['products']['item']['price'])?isset($data['products']['item']['price']):0;
echo $price;
$priceTow=isset($data['products']['item']['price'])??0;
echo $priceTow;
```
- Using data_get()
```php
	$amount=data_get($data,'products.item.price');
    echo $amount;
```
- Setting a default value when key doesn't exists.
```php
$amount=data_get($data,'products.item.price',0);
echo $amount;
```
## Laravel count/withcount
Don't forget eager loading isn't just for grabbing relational models. You can also
use it for fetching relational data such as counts.
<br>
This stops you from having N+1 issues within your applications when you want to display small bits of info.

- This code will load to N+1 issues whith your app.
```php
$posts=Post::with('comments')->get();
foreach ($posts as $post) {
	$countComment = $post->comments->count();
}
```
- Allways Eager load where possible,including counting relationships with models with the flowing.
```php
$posts=Post::withCount('comments')->get();
foreach ($posts as $post) {
	$countComment = $post->comments_count;
}
```
- Laravel remove specific character from a strings.
```php

$string="Football";
//Ftball
Str::remove('o',$string);
Str::of($string)->remove("o");

//Ftba
Str::remove(['o','l'],$string);
Str::of($string)->remove(['o','l']);


