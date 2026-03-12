```
 docker run --rm -it \
   -v "$PWD":/app \
   -w /app \
  node:lts-alpine3.22 \
   sh -c "npm ci --legacy-peer-deps --verbose"



 docker run --rm -it \
   -v "$PWD":/var/www/html \
   -w /var/www/html \
  gilvan/php-apache-oracle:2.2.0 \
  sh -c "composer install --ignore-platform-reqs"

```
