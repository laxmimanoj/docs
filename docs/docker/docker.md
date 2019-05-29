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
- syntax:   
  -- only enabled if the BuildKit backend is used  
  -- defines the location of the Dockerfile builder that is used for building the current Dockerfile    
  -- official releases are available as stable and experimental  
  -- example:    
      \# syntax=docker.io/docker/dockerfile:1  
      \# syntax=docker/dockerfile:1.0.0-experimental  
 - escape:   
    \# escape=\ (backslash) default
      Or  
    \# escape=\` (backtick)  useful for windows 

#### environment variables
- syntax 'ENV variable=value'  
- usage '$variable_name or ${variable_name}'  
- to escape variable conversion to its value, escaping (\\) can be used  
- examples:   
  FROM busybox  
  ENV foo /bar  
  WORKDIR ${foo}   # WORKDIR /bar  
  ADD . $foo       # ADD . /bar  
  COPY \\$foo /quux # COPY $foo /quux  

#### .dockerignore file


### Commands  
-- docker build . [build image]  
-- docker build -f /path/to/a/Dockerfile . [build from specific dockerfile]  
-- docker build -t manoj/myapp:1.0.2 -t manoj/myapp:latest . [build with multiple tags]  
