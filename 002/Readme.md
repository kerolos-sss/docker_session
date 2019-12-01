## If we have made it here we are heros :)

### Simple docker-compose file


Just bulding
```
docker-compose build
```


bringing up the cluster build if necessary

```
docker-compose up
```

```
docker-compose up --build
```

docker-compose stop
[]()




[for a bit of understanding](http://geekyplatypus.com/dockerise-your-php-application-with-nginx-and-php7-fpm/)

I will use this
[https://github.com/thayronarrais/docker-laravel-postgres-nginx](https://github.com/thayronarrais/docker-laravel-postgres-nginx)

Already cloned it 
```
https://github.com/thayronarrais/docker-laravel-postgres-nginx.git
```

[.](#fastcgi_pass_request_headers\son;)


### Install laravell

Now I want to install laravell without all composer hassel 
here I use a docker image with composer as a composer command


```
docker run -u $(id -u) -w=/myproject --rm -v $PWD/application2:/myproject composer composer create-project laravel/laravel . 4.2.*
```
the -u executes the command as the user id specified `id -u` will give a user id eg: `1000`
I don't have `composer` on my pc
this will fail 
```
composer --version
# Command 'composer' not found, but can be installed with:
```




