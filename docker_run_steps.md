docker build -t backend_img .

docker run --name my-postgres -e POSTGRES_PASSWORD=secret -p 5432:5432 -d postgres


docker run -p 80:8080  -e DB_HOST=$(docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' my-postgres) --name backend_cnt -d backend_img

docker build -t frontend_img .
docker run -p 4200:4200  -e BackendIP=$(docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' backend_cnt) --name front_cnt -d frontend_img

docker run -p 4200:4200 --name front_cnt -d frontend_img

# With Docker compose:
docker-compose up
