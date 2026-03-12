# 🐳 Docker
En la carpeta docker se encuentra lo necesario para generar la imagen de docker y la carpeta bindeada al volumen de Docker.

Para generar la imagen:
```bash
# Hay que moverse a la carpeta de docker
cd docker
# Generar la imagen
docker build  -t kafka-jupyter .
# Bindear la carpeta docker-volume
docker run --name kafka-jupyter -v "${PWD}/docker-volume:/opt/local" -p 8888:8888 -p 9092:9092 -p 2181:2181 kafka-jupyter
```