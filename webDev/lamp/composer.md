# [composer](https://getcomposer.org/doc/00-intro.md)
Is a tool for dependency management in PHP. It allows you to declare libraries your project depends on and it will manage (intall/update) them for you.

Composer is **not** a package manager like *apt* or *pacman*. It deals with packages and libraries but per-project basis, installing them in a directory inside your project. By default, it does not install anything globally, but it can.

## Usage
To start, you need `composer.json` in your root project directory.

### `require` key
tells composer which packages your project depends on.
```json
{
    "require": {
        "monolog/monolog": "2.0.*"
    }
}
```

`require` takes an object that maps **package names** (in this case: `monolog/monolog`) to **version constraint** `2.0.*`

composer searches for the right set of files in package "[repositories](https://getcomposer.org/doc/05-repositories.md)" that you register in `repositories` key but since it's unspecified, it uses the default which is [Packagist.org](Packagist.org)

**Package names** consists of a vendor name and the project's name. Often they will be identical. 

In our example, we are requesting the *monolog* package with version constraint `2.0.*` which means any version in the `2.0` development branch, or any version `>=2.0 && <2.1`

### Installing dependencies
To initially install the defined dependencies for your project, run `update`
```bash
~$ composer update
```
which will:
- resolve all dependencies listed in your `composer.json` file and writes all of the packages and their exact versions to the `composer.lock` file, locking your project to those specific versions. You should commit `composer.lock` to your repo.
- it runs `install` command. This downloads the dependencies' files into `vendor` directory in your project; which is the conventional location for all 3rd-party code in a project. 
> So in the example, monolog source files would end up in `vendor/monolog/monolog`

### installing from `composer.lock`
if there's already the `composer.lock` file, it `update` command has been executed before.

Running `install` when `composer.lock` is present, resolves and installs all dependencies that you listen in `composer.json`, but composer uses the exact versions listed in `composer.lock` to ensure package consistency.

So it is recommended that after fetching new changes from your VCS repository, it is recommended to run `install` to make sure the vendor directory is up in sync with your `composer.lock`

```bash
~$ composer install
```

### updating dependencies to their latest versions
`composer.lock` prevents you from automatically getting dependency updates. Using the `update` command will fetch the latest **matching** versions (according to `composer.json`)


## Scripts
Use the `scripts` key to make project-local aliases 
```json
"scripts": {
    "test": "./vendor/bin/phpunit tests/"
}
```

You can then use the script by:
```shell
~/proj/dir$ composer test
```
