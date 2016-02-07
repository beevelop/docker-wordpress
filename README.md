[![Travis](https://img.shields.io/travis/beevelop/docker-wordpress.svg?style=flat-square)](https://travis-ci.org/beevelop/docker-wordpress)
[![Docker Pulls](https://img.shields.io/docker/pulls/beevelop/wordpress.svg?style=flat-square)](https://links.beevelop.com/d-wordpress)
[![ImageLayer](https://badge.imagelayers.io/beevelop/wordpress:latest.svg)](https://imagelayers.io/?images=beevelop/wordpress:latest)
[![Beevelop](https://links.beevelop.com/honey-badge)](https://beevelop.com)

# WordPress for Docker on Steroids

Based on the [official WordPress](https://hub.docker.com/_/wordpress/) image this image fully automates your WordPress installation with the help of [wp-cli](http://wp-cli.org/).

## Run the image
```bash
# Start a MySQL container first
docker run -d -e MYSQL_ROOT_PASSWORD=un1c0rn --name mysql mysql

# Start the WordPress container with 2 plugins and the 'responsive' theme
docker run -d -p 8080:80 \
           -e SITE_URL=http://yoursite.com \
           -e WORDPRESS_PLUGINS="jetpack;wordfence" \
           -e WORDPRESS_ACTIVE_THEME=responsive \
           -e WORDPRESS_THEMES="responsive" \
           --link mysql:mysql beevelop/wordpress:latest
```

## Use as base image
This image is optimized to be used as a base image. You can simply override all ENVs in you own Dockerfile to make your own tailored image.
```Dockerfile
FROM beevelop/wordpress:latest

# e.g. copy your own theme or plugins
# this is quite awesome for CI solutions with continuous deployment in mind
COPY ./ /usr/src/wordpress/wp-content/themes/my-theme/

# you can simply override all the ENVs from the configuration chapter
ENV WORDPRESS_PLUGINS "password-protected;wordfence"
ENV WORDPRESS_ACTIVE_THEME "my-theme"
```

## Configuration
- `SITE_URL` (defaults to `https://example.com`)
- `SITE_TITLE` (defaults to "DockerPress")
- `WORDPRESS_PLUGINS` (defaults to `"hello-dolly"`): Semicolon-separated list of plugins to install and activate
  + e.g. `WORDPRESS_PLUGINS="wordfence;jetpack;hello-dolly"`
- `WORDPRESS_THEMES` (defaults to `"twentysixteen;twentyfifteen"`): Semicolon-separated list of themes to install
- `WORDPRESS_ACTIVE_THEME` (defaults to `twentysixteen`): This theme gets activated on initialization
- `ADMIN_USER` (defaults to `docker`)
- `ADMIN_EMAIL` (defaults to `changeme@example.com`)
- `ADMIN_PASSWORD` (defaults to `Un1c0rn`)
