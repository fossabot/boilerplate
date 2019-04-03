# Laravel/AdminLTE Boilerplate

![Package](https://img.shields.io/badge/Package-sebastienheyd%2Fboilerplate-lightgrey.svg)
[![Build Status](https://scrutinizer-ci.com/g/sebastienheyd/boilerplate/badges/build.png?b=master)](https://scrutinizer-ci.com/g/sebastienheyd/boilerplate/build-status/master)
[![StyleCI](https://github.styleci.io/repos/86598046/shield?branch=master)](https://github.styleci.io/repos/86598046)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/sebastienheyd/boilerplate/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/sebastienheyd/boilerplate/?branch=master)
![Laravel](https://img.shields.io/badge/Laravel-5.8.x-green.svg)
![Nb downloads](https://img.shields.io/packagist/dt/sebastienheyd/boilerplate.svg)
![MIT License](https://img.shields.io/github/license/sebastienheyd/boilerplate.svg)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fsebastienheyd%2Fboilerplate.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fsebastienheyd%2Fboilerplate?ref=badge_shield)

This package is to be served as a basis for a web application. It allows you to access to an administration panel to
manage users, roles and permissions.

For other Laravel versions :
[5.7](https://github.com/sebastienheyd/boilerplate/blob/5.7/README.md) /
[5.6](https://github.com/sebastienheyd/boilerplate/blob/5.6/README.md) /
[5.5](https://github.com/sebastienheyd/boilerplate/blob/5.5/README.md) /
[5.4](https://github.com/sebastienheyd/boilerplate/blob/5.4/README.md)

## Features

* Backend theme [Admin LTE](https://almsaeedstudio.com/)
* Css framework [Bootstrap 3](http://getbootstrap.com/)
* Additional icons by [Font Awesome](http://fontawesome.io/)
* Role-based permissions provided by [santigarcor/laratrust](https://github.com/santigarcor/laratrust)
* Forms & Html helpers by [laravelcollective/html](https://github.com/laravelcollective/html)
* Menu dynamically builded by [lavary/laravel-menu](https://github.com/lavary/laravel-menu)
* Menu items activated by [hieu-le/active](https://github.com/letrunghieu/active)
* Server-side datatables methods provided by [yajra/laravel-datatables](https://github.com/yajra/laravel-datatables)
* Image manipulation by [intervention/image](https://github.com/intervention/image)
* Localized English / French / Spanish / Turkish

## Installation

1. In order to install Laravel/AdminLTE Boilerplate run :

```
composer require sebastienheyd/boilerplate
```

2. Run the command below to publish assets, views, lang files, ...

```
php artisan vendor:publish --provider="Sebastienheyd\Boilerplate\BoilerplateServiceProvider"
```

3. After you set your database parameters in your ```.env``` file run :

```
php artisan migrate
```

**Optional**

If you want to quickly test your Laravel application.

```
php artisan serve
```

Now you can point your browser to [http://localhost:8000/](http://localhost:8000/) you will see buttons on the top right
of the Laravel's default page. Click on Login or Register to access the administration panel.

## Configuration

Configuration files can be found in `config/boilerplate` folder.

* [`app.php`](src/config/app.php) : name of the application (only backend), admin panel prefix,
redirection after login (see comments in file), AdminLTE skin and more...
* [`auth.php`](src/config/auth.php) : overriding of `config/auth.php` to use boilerplate models instead
of default Laravel models. Allow you to define if users can register from login page and which role will be assigned
to a new user.
* [`laratrust.php`](src/config/laratrust.php) : overriding of Laratrust (package santigarcor/laratrust)
default config.
* [`menu.php`](src/config/menu.php) : dashboard and menu classes

### Dashboard

You can define your own controller to display the dashboard. To do this, set the `dashboard` parameter in the
configuration file `config/boilerplate/menu.php`.

### Adding items to the menu

To add an item to the menu, nothing simpler, use the `artisan boilerplate:menuitem` command provided with boilerplate.

This command will generate the classes needed to generate the menu item in the `app/Menu` folder.

```bash
php artisan boilerplate:menuitem {name} {-s} {-o=100}
```

| option / argument | description |
|---|---|
| name | Class name to generate |
| -s --submenu | Menu item must have sub item(s) |
| -o --order | Menu item order in the backend menu |

Once generated, the files can be edited to customize the item, it's quite easy to understand.

You can also add a provider by adding its class name to the list of providers in the configuration file
`config/boilerplate/menu.php`. This can be useful if you are developing a package that is based on boilerplate.

For more information, see the documentation of the following packages:

- [lavary/laravel-menu](https://github.com/lavary/laravel-menu)
- [hieu-le/active](https://github.com/letrunghieu/active)

### Loading plugins assets

By default, only jQuery, bootstrap 3, Font Awesome and AdminLTE scripts and css are loaded.

To load and use plugins like datatable, datepicker, icheck, ... you can use "loaders". These are blade templates
prepared to add the loading of scripts and styles for a plugin.

For example, you want to use a datepicker on a text field :

```blade
@include('boilerplate::load.datepicker')
@push('js')
    <script>
        $('.daterangepicker').daterangepicker();
        $('.datepicker').datepicker();
    </script>
@endpush
```

Here `@include('boilerplate::load.datepicker')` will load scripts and styles to allow usage of datepicker. After that
you can push your scripts on the `js` stack (or styles on the `css` stack).

Available loaders are :

* [`boilerplate::load.datatables`](src/resources/views/load/datatables.blade.php) :
[Datatables](https://www.datatables.net/) -
[Example](src/resources/views/plugins/demo/datatables.blade.php)
* [`boilerplate::load.datepicker`](src/resources/views/load/datepicker.blade.php) :
[Datepicker](https://github.com/uxsolutions/bootstrap-datepicker) &
[DateRangePicker](https://github.com/dangrossman/bootstrap-daterangepicker) -
[Example](src/resources/views/plugins/demo/datepicker.blade.php)
* [`boilerplate::load.icheck`](src/resources/views/load/icheck.blade.php) :
[iCheck](http://icheck.fronteed.com/) -
[Example](src/resources/views/plugins/demo/icheck.blade.php)
* [`boilerplate::load.select2`](src/resources/views/load/select2.blade.php) :
[Select2](https://select2.github.io/) -
[Example](src/resources/views/plugins/demo/select2.blade.php)
* [`boilerplate::load.moment`](src/resources/views/load/moment.blade.php) :
[MomentJs](http://momentjs.com/)
* [`boilerplate::load.fileinput`](src/resources/views/load/fileinput.blade.php) :
[Bootstrap FileInput](http://plugins.krajee.com/file-input)

More will come...

Some plugins are loaded by default :

* [Bootbox](https://github.com/makeusabrew/bootbox) -
[Example](src/resources/views/plugins/demo/bootbox.blade.php)
* [Notify](https://github.com/mouse0270/bootstrap-notify) -
[Example](src/resources/views/plugins/demo/notify.blade.php)

You can see examples on the default dashboard.

### Language

By default the language used by boilerplate is the application language declared into `config/app.php` (locale). You can
define another language only for the back-office by setting `locale` parameter in `config/boilerplate/app.php`.  
Supported language are English, French, Spanish and Turkish.

When you run `php artisan vendor:publish --provider="Sebastienheyd\Boilerplate\BoilerplateServiceProvider"`, only the
language files for form validation are copied for supported languages. Thanks to
[caouecs/Laravel-lang](https://github.com/caouecs/Laravel-lang) package !

You can translate into a language not yet supported by copying the
[`src/resources/lang/boilerplate`](src/resources/lang/boilerplate) folder content into
`resources/lang/vendor/boilerplate` folder. After that, copy or rename one of the language folders in the new language
folder to create. All you have to do is translate. If you want to share the language you have added, don't hesitate to
make a pull request.

### Routes

Routes are loaded from the file [`boilerplate.php`](src/routes/boilerplate.php).

A default prefix `admin` is set into the config file [`app.php`](src/config/app.php), this is why
boilerplate is accessible by /admin url. You can set an empty prefix if you remove the default route / defined in
`routes/web.php`

## Package update

Boilerplate comes with assets such as Javascript, CSS, and images. Since you typically will need to overwrite the assets
every time the package is updated, you may use the ```--force``` flag :

```
php artisan vendor:publish --provider="Sebastienheyd\Boilerplate\BoilerplateServiceProvider" --tag=public --force
```

To auto update assets each time package is updated, you can add this command to `post-autoload-dump` into the
file `composer.json` at the root of your project.


```json
{
    "scripts": {
        "post-autoload-dump": [
            "@php artisan vendor:publish --provider=\"Sebastienheyd\\Boilerplate\\BoilerplateServiceProvider\" --tag=public --force -q",
        ]
    }
}
```

If needed, you can force update for these tags : ```config```, ```lang```, ```public```

| tag | description | destination path |
|---|---|---|
| config | Configuration files | app/config/boilerplate |
| lang | Laravel default lang files for form validation | ressources/lang |
| public | Public assets, you must update it after each package update | public/assets/vendor/boilerplate |

## Tests / Coding standards

This package is delivered with a `Makefile` used to launch checks for the respect of coding standards and the unit tests

Just call `make` to see the list of commands.

### Laravel Dusk functionnal tests

This package is also delivered with functional tests using [Laravel Dusk](https://laravel.com/docs/dusk)

After installing Laravel, Laravel Dusk and configuring your database, you can start the tests with the following command :

```
php artisan dusk vendor/sebastienheyd/boilerplate/tests/DuskTest.php
```

**Important** : Never launch tests with Laravel Dusk if you have data in your database,  Dusk will wipeout all your datas

## Troubleshooting

### Dates localization

Since Laravel 5.8, this package use [Carbon 2](https://carbon.nesbot.com/docs/#api-localization) instead of [Jenssegers/Date](https://github.com/jenssegers/date) to translate dates.

Date format now use the format of momentjs. To translate your dates, you must now use the Carbon 2 class method `isoFormat`
instead of `format`

See [Carbon 2 documentation](https://carbon.nesbot.com/docs/#api-localization)

### Migration error

MySQL < v5.7.7 or MariaDB

When you run `php artisan migrate` and you hit this error :

```
[PDOException]
  SQLSTATE[42000]: Syntax error or access violation: 1071 Specified key was too long; max key length is 767 bytes
```

This is an error from a change since Laravel 5.4 : [see here](https://laravel-news.com/laravel-5-4-key-too-long-error)

To correct this, two possibilities :

- Define `utf8` instead of `utf8mb4` as default database charset and `utf8_unicode_ci` instead of
`utf8mb4_unicode_ci` as default database collation.

- Edit your `app/Providers/AppServiceProvider.php` file and define a default string inside the boot method :

```php
use Illuminate\Support\Facades\Schema;

public function boot()
{
    Schema::defaultStringLength(191);
}
```

## License

This package is free software distributed under the terms of the [MIT license](LICENSE.md).


[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fsebastienheyd%2Fboilerplate.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fsebastienheyd%2Fboilerplate?ref=badge_large)