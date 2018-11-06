# Simple WordPress Site

This is a project that creates a simple WordPress site using a docker-compose setup.

You can also use it to build a docker image suitable for running WordPress elsewhere.

To run the dev setup:
```
docker-compose up -d
```

Then visit [localhost:8080](http://localhost:8080) sometime later. Login at [localhost:8080/wp/wp-admin](http://localhost:8080/wp/wp-admin) as `admin:admin`.

To build and push the production image (contains code and composer dependencies already installed):

```
docker-compose -f docker-compose.yml -f docker-compose.production.yml build
docker-compose -f docker-compose.yml -f docker-compose.production.yml push
```

That will then be available as a public docker image: `outlandish/cola-simple-wordpress-site`