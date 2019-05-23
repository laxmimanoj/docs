# Docker
## Dockerfile reference
### Notes
#### working/theory/options
- build cache is only used from images that have a local parent chain or with images loaded with 'docker load'
- use '--cache-from' to load image cache from other registries
- to use 'buildkit' backend to build images set an environment variable DOCKER_BUILDKIT=1 on the CLI before invoking docker build

#### format
\# Comment  
INSTRUCTION arguments

#### parser directives
- \# directive=value 
- Once a comment, empty line or builder instruction has been processed, Docker no longer looks for parser directives. Therefore, all     parser directives must be at the very top of a Dockerfile.
- Supported parser directives
-- syntax
-- escape

### Commands  
-- docker build . [build image]  
-- docker build -f /path/to/a/Dockerfile . [build from specific dockerfile]  
-- docker build -t manoj/myapp:1.0.2 -t manoj/myapp:latest . [build with multiple tags]  
