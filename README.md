# setup
setup and tutorials

Be familiar with the followings:

- routes
- filters
- listeners
- controllers
- models
- templating
- validation

Checklist:

https://github.com/chiraggude/awesome-laravel

Laravel Cheat Sheet:

http://cheats.jesse-obrien.ca/

To Read:

https://daylerees.com/codesmart/


Composer Cheat Sheet:

http://composer.json.jolicode.com/


If you don’t want it to install development dependencies, then you can use the following switch.

composer update --no-dev

use the composer self-update command to update the Composer binary itself

There are more commands like --dev --save-dev


If you'd like to create your own configuration files, then simply drop them in the config directory. Laravel will load them automatically and will allow to you use them in the same way as its own configuration files. When writing applications for others, be sure to add as much configuration as possible. It's great when you can get an application to work your way.



If a third party package comes with its own configuration files, simply use php artisan vendor:publish to copy them into your configuration directory.
