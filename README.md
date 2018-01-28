# Usage
## Create Docker Network
docker network create --driver bridge ulbora_bridge

## Run Containers on Network

### Nginx
docker run --restart=always --name ulboralabs-1-nginx -p 80:80 --log-opt max-size=50m /
 -v /nginx-conf/nginx.conf:/etc/nginx/nginx.conf:ro -v /nginx-site-conf:/etc/nginx/conf.d:ro /
 -d ulboralabs/ulboralabs-nginx

### Oauth2
docker run --network=ulbora_bridge -p 3000:8080 --name oauth2 --log-opt max-size=50m --env /
DATABASE_HOST=somehost --env DATABASE_USER_NAME=someUser --env DATABASE_USER_PASSWORD=somePassword /
--env DATABASE_NAME=ulbora_oauth2_server --env DATABASE_POOL_SIZE=5 --env /
AUTHENTICATION_SERVICE=http://user:8080/rs/user/login --env PORT=8080 --restart=always -d ulboralabs/oauth2server sh

### User
docker run --network=ulbora_bridge --name user --log-opt max-size=50m --env DATABASE_HOST=someHost /
--env DATABASE_USER_NAME=someUser --env DATABASE_USER_PASSWORD=somePassword --env /
DATABASE_NAME=ulbora_user_service --env DATABASE_POOL_SIZE=5 --env OAUTH2_VALIDATION_URI=http://oauth2:8080/rs/token/validate /
--env PORT=8080 --restart=always -d ulboralabs/userservice sh

