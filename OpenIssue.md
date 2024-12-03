1. Problem 1

root@iZf8ziznc480ukgkuqhah0Z:/www/wwwroot/magicdata# sudo php artisan migrate
Migrating: 2024_11_07_072305_create_prevent_nbs_record_update_when_release_is_specific_value_trigger

   Illuminate\Database\QueryException 

  SQLSTATE[HY000]: General error: 1419 You do not have the SUPER privilege and binary logging is enabled (you *might* want to use the less safe log_bin_trust_function_creators variable) (SQL: 
            CREATE TRIGGER prevent_update_when_release_is_locked
            BEFORE UPDATE ON nbs_records
            FOR EACH ROW
            BEGIN
                IF OLD.status = "locked" && NEW.status="locked" THEN
                    SIGNAL SQLSTATE "45000"
                    SET MESSAGE_TEXT = "Cannot update record when release is locked";
                END IF;
            END;
        )


2. Problem 2


Seeded:  Database\Seeders\Indicator\nbs\monthly\NbsMonthlyCountryIndicatorSeeder (14.92ms)

   Illuminate\Contracts\Container\BindingResolutionException 

  Target class [Database\Seeders\data\nbs\monthly\NbsMonthlyPMICountryDataSeeder] does not exist.

  at vendor/laravel/framework/src/Illuminate/Container/Container.php:879
    875▕ 
    876▕         try {
    877▕             $reflector = new ReflectionClass($concrete);
    878▕         } catch (ReflectionException $e) {
  ➜ 879▕             throw new BindingResolutionException("Target class [$concrete] does not exist.", 0, $e);
    880▕         }
    881▕ 
    882▕         // If the type is not instantiable, the developer is attempting to resolve
    883▕         // an abstract type such as an Interface or Abstract Class and there is

      +8 vendor frames 
  9   database/seeders/TestSeeder.php:45
      Illuminate\Database\Seeder::call()

      +22 vendor frames 
  32  artisan:37
      Illuminate\Foundation\Console\Kernel::handle()