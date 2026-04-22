# phpyh/php

PHP Docker images for development and CI, built on top of `php:<version>-cli-alpine`.

## Images

Published every Monday to `ghcr.io/phpyh/php` for `linux/amd64` and `linux/arm64`.

| Tag                     | PHP |
|-------------------------|-----|
| `ghcr.io/phpyh/php:8.2` | 8.2 |
| `ghcr.io/phpyh/php:8.3` | 8.3 |
| `ghcr.io/phpyh/php:8.4` | 8.4 |
| `ghcr.io/phpyh/php:8.5` | 8.5 |

## What's included

### PHP extensions

- `opcache`
- `uv`
- `pcntl`
- `sockets`
- `intl`
- `bcmath`
- `pgsql`
- `pdo_pgsql`
- `xdebug`

Xdebug client host is pre-configured to `host.docker.internal`.

### Global Composer packages

- [php-cs-fixer](https://github.com/PHP-CS-Fixer/PHP-CS-Fixer)
- [phpstan](https://phpstan.org) + `phpstan-strict-rules`, `phpstan-phpunit`
- [rector](https://getrector.com)
- [infection](https://infection.github.io)
- [composer-dependency-analyser](https://github.com/shipmonk-rnd/composer-dependency-analyser)
- [composer-normalize](https://github.com/ergebnis/composer-normalize)

`COMPOSER_HOME` is set to `/composer`, and `/composer/vendor/bin` is added to `PATH` —
global tools are available as commands without full path. The directory is owned by `dev`,
so `composer global require` works without `sudo`.

### System tools

`make`, `git`, `unzip`

### User

The default user is `dev` (UID `10001`, GID `10001`). 
The UID and GID can be overridden at build time via `--build-arg UID=... --build-arg GID=...`
to match the host user and avoid file permission issues with mounted volumes.

## Usage

```yaml
# docker-compose.yml
services:
  app:
    image: ghcr.io/phpyh/php:8.5
    volumes:
      - .:/app
      - ~/.composer/cache:/composer/cache
    working_dir: /app
```

## License

MIT License — see [LICENSE](LICENSE) for details.
