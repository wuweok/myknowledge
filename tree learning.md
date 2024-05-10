首先我们将基于menu， 不动model 复制一个menu

1.  php artisan admin:make MyMenuController --model=Encore\\Admin\\Auth\\Database\\Menu

2.  $router->resource('mymenus', MyMenuController::class);

3. test http://magicdata.test/admin/mymenus  ok


