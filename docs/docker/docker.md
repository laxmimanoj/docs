# Docker
## Dockerfile reference

Commands:  
-- docker build . [build image]
-- docker build -f /path/to/a/Dockerfile . [build from specific dockerfile]
-- docker build -t manoj/myapp:1.0.2 -t manoj/myapp:latest . [build with multiple tags]

- build cache is only used from images that have a local parent chain or with images loaded with 'docker load'
- use '--cache-from' to load image cache from other registries
