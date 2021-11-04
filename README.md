# CustomEntityBundle

[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/akeneo-labs/CustomEntityBundle/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/akeneo-labs/CustomEntityBundle/?branch=master)
[![Build Status](https://travis-ci.org/akeneo-labs/CustomEntityBundle.svg?branch=master)](https://travis-ci.org/akeneo-labs/CustomEntityBundle)

Facilitates the creation of PIM reference data and related views in the PIM.

For more information, please see http://docs.akeneo.com/

## THIS FORK
This fork is intended to allow a temporary patch, expecting an update from the offical repository.

## Requirements

| CustomEntityBundle   | Akeneo PIM Community Edition |
|:--------------------:|:----------------------------:|
| v5.0.*               | v5.0.*                       |


## Installation
You can install this fork by adding the repository section in your composer.json file:

```bash
#composer.json
        "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/vincentlemire/custom-entity-bundle"
        }
    ],
    ...
    "require": {
        "akeneo/pim-community-dev": "^5.0.0",
        "akeneo-labs/custom-entity-bundle" : "5.0.x-dev",
        ...
    },


```

Then add the following lines **at the end** of your config/routes/routes.yml :

```yaml
    pim_customentity:
        prefix: /reference-data
        resource: "@PimCustomEntityBundle/Resources/config/routing.yml"
```

and enable the bundle in the `config/bundles.php` file:

```php
    return [
        // ...
        Pim\Bundle\CustomEntityBundle\PimCustomEntityBundle::class => ['all' => true]
    ];
```

If your installation is already set up, you have to run the following command in order to add the quick export job:
 
```bash
    php bin/console akeneo:batch:create-job "Akeneo Mass Edit Connector" "csv_reference_data_quick_export" "quick_export" "csv_reference_data_quick_export" '{"delimiter": ";", "enclosure": "\"", "withHeader": true, "filePath": "/tmp/reference_data_quick_export.csv"}'
```

## Documentation

The reference data documentation can be found in the 
[PIM documentation](https://docs.akeneo.com/4.0/manipulate_pim_data/catalog_structure/creating_a_reference_data.html).

Detailled information can be found in the [bundle documentation](docs/index.md).

## Run the Tests

### Unit tests

```bash
    $ composer install
    $ vendor/bin/phpspec run
```

### Code style

```bash
    $ composer install
    $ vendor/bin/php-cs-fixer fix -v --diff --config .php_cs.php
```

### PHPUnit

* Install an Akeneo PIM with the CustomEntityBundle
* Copy `Tests/Resources/phpunit.xml` to project root
* Copy `Tests/Resources/.env.test` to project root, and edit accordingly to your config
* Copy `Tests/Resources/bundles.php` or `Tests/Resources/bundles_ee.php` (depending on your PIM version) content in the `config/bundles.php` file

Then:

```bash
    $ php bin/console cache:warmup --env=test

    If you're on EE Edition :
    $ php bin/console pim:installer:db --env=test --catalog vendor/akeneo/pim-enterprise-dev/src/Akeneo/Platform/Bundle/InstallerBundle/Resources/fixtures/minimal
    Else :
    $ php bin/console pim:installer:db --env=test --catalog vendor/akeneo/pim-community-dev/src/Akeneo/Platform/Bundle/InstallerBundle/Resources/fixtures/minimal

    $ vendor/bin/phpunit
```

## Contributing

If you want to contribute to this open-source project,
thank you to read and sign the following [contributor agreement](http://www.akeneo.com/contributor-license-agreement/)
