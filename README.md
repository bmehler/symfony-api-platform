# API Platform with Symfony 5.4

## Getting the Project

To install clone the github repository

```php
git clone https://github.com/bmehler/symfony-api-platform.git
```

Change to the cloned folder and use the composer

```php
cd symfony-api-platform
composer install
```

## To do in Symfony

Change the following line in .env to use a database

```php
DATABASE_URL="mysql://<db_user>:<db_password@<db_host>/<db_name>?serverVersion=5.7"

For example:
db_user = root
db_password = root
db_host = 127.0.0.1:3306
db_name = employees
```
Do following to work to connect your database an create a table

```php
php bin/console doctrine:database:create
php bin/console make:migration
php bin/console doctrine:migrations:migrate
```

You can create a virtualhost like I do
```php
<VirtualHost *:80>
    DocumentRoot "<your path to public folder>"
    ServerName employeeapi.local.com
    <Directory "<your path to public folder>">
        AllowOverride All
        Order Allow,Deny
        Allow from All
    </Directory>
</VirtualHost>
```

## Open RestApi Routes
```php
<your virtualhost>/api
```
## GraphQl Support 

```php
<your virtualhost>/api/graphql
```
Get all Customers
```php
{
  customers {
   totalCount
    edges {
      node {
        firstname
        surname
        street
        city
        country
        phone
        email
      }
    }
  }
}
```

Do a query
```php
query Customer {
  customers {
    totalCount
    edges {
      node {
        firstname
      }
    }
  }
}
```

Get Customer by Id
```php
{
  customer(id: "/api/customers/1") {
    firstname
    surname
    street
    city
    country
    phone
    email
  }
}
```
Get a Customer with Variable
```php
query GetCustomerById($id: ID!) {
  customer(id: $id) {
    firstname
    surname
    street
    city
    country
    phone
    email
  }
}

with variables
{
  "id": "/api/customers/1"
}
```