## Basic Docker Container for php7.4-fpm

### Based on: PHP 7.4-fpm

### Installed extension: 
        - pdo_mysql 
        - mbstring 
        - zip 
        - exif 
        - pcntl 
        - sockets 
        - json 
        - bcmath
        - gd

### Configuration

| Key | Default | Possible  Value | 
|:-----:|:-------:|------
| BUILD  | PROD | PROD / DEV
| DEBUG_IP | 0.0.0.0 | {ip}
| DEBUG_PORT | 9999 | {integer}
| DEBUG_PORT | ddebug | {string}


### Example

    - docker build -t php-custom-docker . --build-arg BUID=DEV 