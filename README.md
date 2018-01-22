# Usage
docker run --name ulboralabs-1-nginx -p 80:80 /
 -v /nginx-conf/nginx.conf:/etc/nginx/nginx.conf:ro /
 -v /nginx-site-conf:/etc/nginx/conf.d:ro -d ulboralabs/ulboralabs-nginx

# Ulbora CMS
docker run --restart=always -p 3001:8080 --name kenwilliamson.com \
--env DOCKER_ULBORACMS_DATABASE_NAME=ken-ulboracmsdb \
--link ulboramongo:mongo -d  \
ulboralabs/ulboracms sh


# nginx
docker run --restart=always --name ulboralabs-1-nginx -p 80:80 -v /nginx-conf/nginx.conf:/etc/nginx/nginx.conf:ro /
-v /nginx-site-conf:/etc/nginx/conf.d:ro / 
-d ulboralabs/ulboralabs-nginx