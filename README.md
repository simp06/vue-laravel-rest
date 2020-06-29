# Crud de Items y filtros , en vue, portal de admin y  portal publico 

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Installation

``` bash
# clone el repo
$ git clone https://github.com/coreui/coreui-free-vue-laravel-admin-template.git my-project

# ir al directorio laravel
$ cd my-project/laravel

# instalar las dependencias de laravel
$ composer install

# instalar las dependendias de vue
$ npm install
```

### Configuracion de base de datos


Copiar archivo  ".env.example", cambiar el nombre a  ".env".
Then in file ".env" replace this database configuration:
* DB_CONNECTION=mysql
* DB_HOST=127.0.0.1
* DB_PORT=3306
* DB_DATABASE=database
* DB_USERNAME=root
* DB_PASSWORD=


### Siguiente paso 

``` bash
# en el directorio laravel 
# generar laravel APP_KEY
$ php artisan key:generate

# generar jwt secret
$ php artisan jwt:secret

# correr migraciones y  seeders
$ php artisan migrate:refresh --seed

```

```bash
#  ir a coreui
$ cd ../coreui

# install app's dependencies
$ npm install

```

``` bash
# Regresar al directorio laravel
$ cd ../laravel

# generar mixing
$ npm run dev

# y repetir el mixing
$ npm run dev
```

## Ejecutar laravel

``` bash
# start local server
$ php artisan serve

```
## Ejecutar Admin
Abrir localhost direccion: [localhost:8000/admin](localhost:8000/admin)  
 
* Username : admin
* Password: password

--- 

## Componentes y controladores

### Componentenes:
* CreateSoftware
* EditSoftware
* Softwares
### Controladores:
* SoftwareController
* ComparaController


#### SoftwareController
Controlador usado para la api de software

#### ComparaController
Controlador usado para la parte publica 

### Filtros 
Los filtros fueron creados por separados es decir existen filtros de lenguajes y de funcionalidades, no se considero como una sola entedidad


## Links

**Admin**

* <localhost:port/admin>


**Publica**

* <localhost:port/compara>

## Copyright and license

copyright 2018 creativeLabs Łukasz Holeczek. Code released under [the MIT license](https://github.com/coreui/coreui-free-laravel-admin-template/blob/master/LICENSE).
There is only one limitation you can't can’t re-distribute the CoreUI as stock. You can’t do this if you modify the CoreUI. In past we faced some problems with persons who tried to sell CoreUI based templates.

