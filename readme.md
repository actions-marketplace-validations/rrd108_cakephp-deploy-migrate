# CakePHP Deploy

## Config example:

```
name: CakePHP Deploy
on:
    create:
        tags:
            - "*"

jobs:
    build:
        name: CakePHP Deploy
        runs-on: ubuntu-latest
        steps:
            -   name: Checkout Repository
                uses: actions/checkout@master
            -   name: Setup Enviroment
                uses: shivammathur/setup-php@v2
                with:
                    php-version: '7.4'
                    extensions: intl, mbstring, simplexml, pdo
            -   name: Install Packages in the temporary container
                run: composer install --no-dev
            -   name: Deploy to Server
                uses: rrd108/cakephp-deploy-migrate@master
                with:
                    user: 'ssh user name : rrd'
                    host: 'ssh server name : server.com'
                    port: 'ssh port : 22'
                    path: 'path on server to deploy : ../../web/'
                    owner: 'username on server who is the owner : web1'
                env:
                    DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
```
