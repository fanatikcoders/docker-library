## Supported tags and respective Dockerfile links:

### Wordpress [Docker Hub](https://hub.docker.com/r/fanatikcoders/wordpress/)

- `4.9-php7.0-apache` [(wordpress/4.9/php7.0/apache/Dockerfile)](https://github.com/fanatikcoders/docker-library/blob/master/wordpress/4.9/php7.0/apache/Dockerfile)

### PHP [Docker Hub](https://hub.docker.com/r/fanatikcoders/php/)

- `7.0-apache` [(php/7.0/apache/Dockerfile)](https://github.com/fanatikcoders/docker-library/blob/master/php/7.0/apache/Dockerfile)
- `7.1-apache` [(php/7.1/apache/Dockerfile)](https://github.com/fanatikcoders/docker-library/blob/master/php/7.1/apache/Dockerfile)
- `7.2-apache` [(php/7.2/apache/Dockerfile)](https://github.com/fanatikcoders/docker-library/blob/master/php/7.2/apache/Dockerfile)

## Configuring xdebug

- Create an alias for remote IP:

```sh
sudo ifconfig lo0 alias 10.254.254.254 255.255.255.0
```

- In docker-compose.yml enable XDEBUG:

```yml
web:
  environment:
    PHP_XDEBUG_ENABLED: 1 # Set 1 to enable.
    XDEBUG_CONFIG: remote_host=10.254.254.254 remote_port=9000 idekey=phpstorm remote_log=/tmp/xdebug.log
```

- You can add a script to bring up the alias at startup:

This may require sudo. We don't copy it to `~/Library/LaunchAgents` because needs to be run as sudo?

```
curl https://raw.githubusercontent.com/fanatikcoders/docker-library/master/assets/autorun_alias_for_lo.plist >> /Library/LaunchDaemons/com.rbngzlv.docker_10254254254_alias.plist
```

## Configure PHP Storm:

- PHP Interpreter:

![PHPStorm PHP Interpreter](https://github.com/fanatikcoders/docker-library/blob/master/assets/images/phpstorm_php_interpreter.png)

- DBGp proxy:

![PHPStorm DBGp proxy](https://github.com/fanatikcoders/docker-library/blob/master/assets/images/phpstorm_dbgp_proxy.png)

*Note:* Remind to click to listen PHP Debug connections and check that firewall is not rejecting connections

## Other

- From inside docker container you can contact to host:

```
ping docker.for.mac.host.internal
```

- To get the IP of your machine:

```
ifconfig en0 | awk '/ *inet /{print $2}'
```

- To get host docker bridge IP:

```
docker network inspect bridge |awk '/"Gateway"/ {gsub ("\"","") ;print $2}'
```
