# PHP Database Manager

This is a simple library for managing database connections, results pagination and building queries in PHP.

## Usage

To use this library just follow the examples below:

#### Database
```php
<?php

require 'vendor/autoload.php';

use Unimed\DatabaseManager\Database;

//DATABASE CREDENTIALS
$dbHost = 'localhost';
$dbName = 'database';
$dbUser = 'root';
$dbPass = 'pass';
$dbPort = 3306;

//CONFIG DATABASE CLASS
Database::config($dbHost,$dbName,$dbUser,$dbPass,$dbPort);

//TABLE INSTANCE
$obDatabase = new Database('table_name');

//SELECT (return a PDOStatement object)
$results = $obDatabase->select('id > 10','name ASC','1','*');

//INSERT (return inserted id)
$id = $obDatabase->insert([
  'name' => 'Unimed'
]);

//UPDATE (return a bool)
$success = $obDatabase->update('id = 1',[
  'name' => 'Unimed2'
]);

//DELETE (return a bool)
$success = $obDatabase->delete('id = 1');

```

#### Pagination
```php
<?php

require 'vendor/autoload.php';

use Unimed\DatabaseManager\Database;
use Unimed\DatabaseManager\Pagination;

//DATABASE CREDENTIALS
$dbHost = 'localhost';
$dbName = 'database';
$dbUser = 'root';
$dbPass = 'pass';
$dbPort = 3306;

//CONFIG DATABASE CLASS
Database::config($dbHost,$dbName,$dbUser,$dbPass,$dbPort);

//TABLE INSTANCE
$obDatabase = new Database('table_name');

//COUNT TOTAL RESULTS
$totalResults = $obDatabase->select('id > 10',null,null,'COUNT(*) as total')->fetchObject()->total;

//CURRENT PAGE
$currentPage  = $_GET['page'] ?? 1;
$itemsPerPage = 10;

//PAGINATION
$obPagination = new Pagination($totalResults,$currentPage,$itemsPerPage);

//SELECT (return a PDOStatement object)
$results = $obDatabase->select('id > 10',null,$obPagination->getLimit());

//PAGES (array)
$pages = $obPagination->getPages();

```

## Requirements

This library needs PHP 7.0 or greater.
