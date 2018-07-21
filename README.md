<h1 align="center">
  Randomly priced games
</h1>
<p align="center">This is a gaming store API, which provides basic functionality for product management </p>

### Prerequisites
 - **Linux/OS X Windows)**
 - [**Git**](https://www.atlassian.com/git/tutorials/install-git)
 - [**Docker**](https://docs.docker.com/engine/installation/)

### Set up
1. Clone this repository using: `git clone https://github.com/WictorT/randomly-priced-games.git`
2. `cd randomly-priced-games`
3. Run `docker-compose build --no-cache` to build images.
4. Copy `.env.dist` into `.env` and configure as you are wiling(better keep default values).
5. Run `docker-compose up` to bring up your containers.
6. Hope containers are up. If yes then run `docker-compose exec php bash` to enter container. Note: Next commands need to be run inside the container
7.
   (inside php container) Generate the SSH keys for JWT:
    
    ``` bash
    mkdir config/jwt
    openssl genrsa -out config/jwt/private.pem -aes256 4096
    openssl rsa -pubout -in config/jwt/private.pem -out config/jwt/public.pem
    ```
    
    In case first ```openssl``` command forces you to input password use following to get the private key decrypted
    ``` bash
    openssl rsa -in config/jwt/private.pem -out config/jwt/private2.pem
    mv config/jwt/private.pem config/jwt/private.pem-back
    mv config/jwt/private2.pem config/jwt/private.pem
    rm config/jwt/private.pem-back
    ```
8. (inside php container) Run `sh setup.sh` if it is the first time you launched the project

You can now access the application here (by default): [http://localhost:3000](http://localhost:3000)

### Launching tests
- To launch tests tests run:
```
docker-compose -f docker/development/docker-compose.yml -f docker/testing/docker-compose.yml -p $(basename $(pwd)) exec php ./vendor/bin/phpunit
```
- To launch tests with code coverage and logging you can use the command:
```
docker-compose -f docker/development/docker-compose.yml -f docker/testing/docker-compose.yml -p $(basename $(pwd)) exec php ./vendor/bin/phpunit --coverage-clover coverage/clover.xml --log-junit coverage/junit.xml
```
this will create a coverage file: [coverage/clover.xml](coverage/clover.xml),
and a logging one: [coverage/junit.xml](coverage/junit.xml)

<h2 align="center"> Thank you! </h2>
<h3> Provided by Victor Timoftii </h3>
