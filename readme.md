# CakePHP Deploy and Migration

## Config example:

```
name: CakePHP Deploy and Migration
on:
    create:
        tags:
            - "*"

jobs:
    build:
        name: CakePHP Deploy and Migration
        runs-on: ubuntu-latest
        steps:
            -   name: Checkout Repository
                uses: actions/checkout@master
            -   name: Setup Enviroment
                uses: shivammathur/setup-php@v2
                with:
                    php-version: '7.4'
                    extensions: intl, mbstring, simplexml, pdo
            -   name: Speed up the packages installation process
                run: composer global require hirak/prestissimo
            -   name: Install Packages
                run: composer install --no-dev
            -   name: Deploy to Server
                uses: rrd108/cakephp-deploy-migrate@cakephp
                with:
                    user: user
                    host: host
                    port: port
                    path: path
                    owner: owner
                env:
                    DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
```
