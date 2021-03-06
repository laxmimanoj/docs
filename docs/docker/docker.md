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
- .dockerignore, if exist, should be at the root directory of the context  
- it is new line separated  
- Examples:  
  \# comment \#ignored  
  temp? \#exclude one-character extension of temp  
  \*/\*/temp* \#exclude two levels below the root  
  temp? \#exclude one-character extension of temp like tempa and tempb  
- ** that matches any number of directories (including zero)  
- ! (exclamation mark) can be used to make exceptions to exclusions  
-  the last line of the .dockerignore that matches a particular file determines whether it is included or excluded  
   Example:    
    *.md  
    !README*.md  
    README-secret.md  
    
    behaves differently than   
    
    *.md  
    README-secret.md  
    !README*.md  
  - we can exclude Dockerfile and .dockerignore but they are still sent to daemon. But are not added to image as part of ADD or COPY instruction  

#### INSTRUCTIONS
##### FROM
##### RUN
##### CMD
##### LABEL
##### EXPOSE
##### ENV
##### ADD
##### COPY
##### ENTRYPOINT
##### VOLUME
##### USER
##### WORKDIR
##### ARG
##### ONBUILD
##### STOPSIGNAL
##### HEALTHCHECK
##### SHELL
### Commands  
-- docker build . [build image]  
-- docker build -f /path/to/a/Dockerfile . [build from specific dockerfile]  
-- docker build -t manoj/myapp:1.0.2 -t manoj/myapp:latest . [build with multiple tags]  

## Filter and Format
The currently supported filters are:  

- dangling (boolean - true or false)  
  docker images --filter "dangling=true"  
- label (label=<key> or label=<key>=<value>)  
  docker images --filter "label=com.example.version=1.0"  
- before (<image-name>[:<tag>], <image id> or <image@digest>) - filter images created before given id or references  
  docker images --filter "before=image1"  
- since (<image-name>[:<tag>], <image id> or <image@digest>) - filter images created since given id or references  
  docker images --filter "since=image3"  
- reference (pattern of an image reference) - filter images whose reference matches the specified pattern  
  docker images --filter=reference='busy*:*libc'  

The formatting option (--format) will pretty print container output using a Go template.  
- docker images --format "{{.ID}}: {{.Repository}}"  
- docker images --format "table {{.ID}}\t{{.Repository}}\t{{.Tag}}"  
- Valid placeholders for the Go template are .ID, .Repository, .Tag, .Digest, .CreatedSince, .CreatedAt, .Size	  
