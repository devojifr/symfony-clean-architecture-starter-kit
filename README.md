
# Symfony Clean Architecture Starter Kit

This project is built from the following stack:
- Symfony 7.1
- PHP >= 8.2

This project is used to have a basic structure of a clean architecture.

Composer is used to manage dependencies.


## Installation

Install my-project with composer

```bash
  cd my-project
  composer install
```

If you want to install Doctrine:
```bash
composer require symfony/orm-pack
composer require --dev symfony/maker-bundle
```
You will need to update Doctrine configuration files.

Update dir, prefix and alias in mappings/app (feel free to choose any folder):
```bash
# config/packages/doctrine.yaml
doctrine:
    ...
        
    orm:
        ...
        mappings:
            App:
                type: attribute
                is_bundle: false
                dir: '%kernel.project_dir%/src/Infrastructure/Entity'
                prefix: 'Infrastructure\Doctrine\Entity'
                alias: Infrastructure
                ...
```

Same for migrations path:
```bash
# config/packages/doctrine_migrations.yaml
doctrine_migrations:
    migrations_paths:
        # namespace is arbitrary but should be different from App\Migrations
        # as migrations classes should NOT be autoloaded
        'DoctrineMigrations': '%kernel.project_dir%/src/Infrastructure/migrations'
    enable_profiler: false
```

If you want to use "make:entity" command, you will see this information:
```bash
! [NOTE] It looks like your app may be using a namespace other than "App".                                             
!                                                                                                                      
!        To configure this and make your life easier, see: https://symfony.com/doc/current/bundles/SymfonyMakerBundle/index.html#configuration
```
The link provided will help you to finish configuration:
https://symfony.com/doc/current/bundles/SymfonyMakerBundle/index.html#configuration

You will need to create the following yml file:
```bash
#config/packages/maker.yaml
when@dev:
  maker:
    root_namespace: 'Infrastructure\Doctrine'
    generate_final_classes: true
    generate_final_entities: false
```
 
## Running Tests

To run tests, run the following command

```bash
  vendor/bin/phpunit
```

