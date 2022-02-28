### 生成一套(也没全用上,policy,form requests就没用上)
```shell
php artisan make:model Flight --migration --controller --factory --seed
```
简写
```shell
php artisan make:model Flight -mfsc 
```

### [If you need to customize the format of your model's timestamps](https://laravel.com/docs/9.x/eloquent#timestamps)

### [Default Attribute Values](https://laravel.com/docs/9.x/eloquent#default-attribute-values)

### [why use "->get()"](https://laravel.com/docs/9.x/eloquent#building-queries)

### [Collections](https://laravel.com/docs/9.x/eloquent#collections)
the reject method may be used to remove models from a collection based on the results of an invoked closure:
```php
$flights = Flight::where('destination', 'Paris')->get();
 
$flights = $flights->reject(function ($flight) {
    return $flight->cancelled;
});
```
Since all of Laravel's collections implement PHP's iterable interfaces, you may loop over collections as if they were an array:
```php
foreach ($flights as $flight) {
    echo $flight->name;
}
```
### [Chunking Results](https://laravel.com/docs/9.x/eloquent#chunking-results)


### [Chunking Using Lazy Collections](https://laravel.com/docs/9.x/eloquent#chunking-results)

### [Cursors](https://laravel.com/docs/9.x/eloquent#cursors)

### [Subquery Selects](https://laravel.com/docs/9.x/eloquent#subquery-selects)

### [Subquery Ordering](https://laravel.com/docs/9.x/eloquent#subquery-selects)


### [Retrieving Single Models / Aggregates](https://laravel.com/docs/9.x/eloquent#retrieving-single-models)
```PHP
use App\Models\Flight;
 
// Retrieve a model by its primary key...
$flight = Flight::find(1);
 
// Retrieve the first model matching the query constraints...
$flight = Flight::where('active', 1)->first();
 
// Alternative to retrieving the first model matching the query constraints...
$flight = Flight::firstWhere('active', 1);
```
Sometimes you may wish to retrieve the first result of a query or perform some other action if no results are found. The firstOr method will return the first result matching the query or, if no results are found, execute the given closure. The value returned by the closure will be considered the result of the firstOr method:
```php
$model = Flight::where('legs', '>', 3)->firstOr(function () {
    // ...
});
```




