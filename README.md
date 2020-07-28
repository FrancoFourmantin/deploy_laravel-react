# Deploy Laravel + React

Aqui vamos a describir los pasos para hacer un correcto deploy de una aplicación web hecha con **Laravel** como RESTful API y **REACT** como front-framework.

### Preparar para producción

1. Subir repositorio a github sin incluir los archivos privados ( .env , node_modules , vendor ) etc.

2. Preparar webpack para produccion( npm run production )
  
### Subir archivos

1. En el servidor donde vayamos a alojar el proyecto debemos tener instalado **composer-npm-php7.4**

2. Vamos a clonar el proyecto

3. Descargamos dependecias (npm install, composer install)

4. Generamos archivo .env con la configuracion necesaria para las variables de entorno

5. Ejecutamos la siguientes lineas:
   1) **php artisan key:generate**
   2) **php artisan cache:clear**
   3) **php artisan config:cache**

6. En la carpeta raiz vamos a generar un archivo .htaccess con la siguientes lineas (para redirigir a la carpeta public como predeterminada).
  ```xml
  <IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteRule ^(.*)$ public/$1 [L]
  </IfModule>
  ```

### Migraciones

  1. Las migraciones se encuentran adentro de database/migrations y sirven para generar la estructura en la base de datos

  2. Correr las migraciones **php artisan migrate**

  3. Si se presenta algun error a la hora de migrar (mySql 1071) se debe modificar **/app/Providers/AppServiceProvider.php**
     ```php
      use Illuminate\Database\Schema\Builder; // Import Builder where defaultStringLength method is defined
      function boot()
      {
        Builder::defaultStringLength(191); // Update defaultStringLength
      }
      ```

  
