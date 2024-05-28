1. generating model classes
   php artisan make:model SeventyCityHouseData;--migration
1.1  with multiple option, see detail with "php artisan make:model --help"
	# Generate a model and a migration, factory, seeder, and controller...
        php artisan make:model Flight -mfsc
1.2 with separate command


2 create factory
   php artisan make:factory SeventyCityHouseDataFactory --model=SeventyCityHouseData
3. create seeder
      php artisan make:seeder SeventyCityHouseDataSeeder
3.1 reference model
    use App\Models\SeventyCityHouseData;
3.2 init seeder.
3.3 seed
php artisan db:seed  --class=SeventyCityHouseDataSeeder


4. API Resources
Function:
	When building an API, you may need a transformation layer that sits between your Eloquent models and the JSON responses that are actually returned to your application's users 
Command:
	php artisan make:resource SeventyCityHouseDataResource
Result: 
	app/Http/Resources/SeventyCityHouseDataResource.php


5. API controller
Command:
	php artisan make:controller Api/SeventyCityHouseDataController

Reuslt:
	app\Http\Controllers\Api\SeventyCityHouseDataController.php

5.1 Add refefernce to Resource and Model
	use App\Models\SeventyCityHouseData;
	use App\Http\Resources\SeventyCityHouseDataResource;
5.2 write index, show etc method
	
6. Add Router
   use App\Http\Controllers\Api\SeventyCityHouseDataController;
   ......
   Route::resource('seventycities', SeventyCityHouseDataController::class)->only([ 'index', 'show']);  
   Route::resource('SeventyCityHouseDatas', SeventyCityHouseDataController::class);

Note: 必须新写法，有些就写法不在支持，会报找不到controller 类。

7. check route
   php artisan route:list

8. test api
   http://magicdata.test/api/seventycities



9.

在SQL中，如果你想将某个字段的所有记录相乘，你可以使用聚合函数PRODUCT（在某些数据库系统中如PostgreSQL）。但是，请注意，不是所有的数据库系统都支持PRODUCT函数。例如，MySQL和SQL Server就没有这个函数。

对于不支持PRODUCT函数的数据库，你可能需要使用其他方法来实现。一种常见的方法是使用EXP和SUM函数结合LN函数（自然对数）来实现。

以下是一些示例：

使用PRODUCT函数（例如：PostgreSQL）:
sql
SELECT PRODUCT(your_column) 
FROM your_table;
使用EXP和SUM结合LN函数（例如：MySQL或SQL Server）:
sql
SELECT EXP(SUM(LN(your_column))) 
FROM your_table;

SELECT EXP(SUM(LN(`month_on`/100)))  FROM `seventy_city_house_data` WHERE 1




5. service

php artisan make:service UserService