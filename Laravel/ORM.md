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


---- to see [Chunking Using Lazy Collections](https://laravel.com/docs/9.x/eloquent#chunking-results)