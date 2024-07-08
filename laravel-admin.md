1. 创建控制器
	php artisan admin:make UserController --model=App\\Models\\User

2. 添加路由
在路由配置文件app/Admin/routes.php里添加一行：
   $router->resource('users', UserController::class)

3.添加菜单栏入口
打开菜单管理页http://localhost:8000/admin/auth/menu，添加对应的menu, 然后就能在后台管理页面的左侧边栏看到用户管理页面的链接入口了。

其中uri填写不包含路由前缀的的路径部分，比如完整路径是http://localhost:8000/admin/demo/users, 那么就填demo/users


4. 导入数据   =>  此办法不可行。 
4.1 创建action （https://laravel-admin.org/docs/zh/2.x/model-table-custom-actions#%E6%99%AE%E9%80%9A%E6%93%8D%E4%BD%9C）
php artisan admin:action User\\ImportUser --name="导入数据"
    此办法不可行。


5. 通过RowAction 来实现。

5.1 形成 action 
  php  artisan admin:action Indicator\\ImportIndicator --grid-row --name="导入数据" 

5.2 add menu action for row
a. add reference 
	use App\Admin\Actions\Indicator\ImportIndicator;

b. bind action 
        $grid->actions(function ($actions) {
            $actions->add(new ImportIndicator());
        });

5.3 call import in handle
5.3.1 add
    use App\Imports\IndicatorsImport;
    use Maatwebsite\Excel\Facades\Excel;
    ......
    Excel::import(new IndicatorsImport, '/home/vagrant/code/magicdata/database/importexcel/indicator1.xlsx');