# @bigloupe/buildpacks-action

![Run action](https://github.com/bigloupe/buildpacks-action/workflows/Run%20action/badge.svg)

Build container image with [Cloud Native Buildpacks](https://buildpacks.io) in GitHub Actions.

```yaml
on: [push]
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2

    - name: Build image
      uses: bigloupe/buildpacks-action@master
      with:
        image: 'foo-app'
        tag: '1.0.0'
        path: 'path/to/foo-app/'
        builder: 'gcr.io/paketo-buildpacks/builder:base'
        env: 'HELLO=WORLD FOO=BAR BAZ'

    - name: Push image
```

> buildpacks v0.18.1 will be executed.

## Inputs
- `image` : (required) Name of container image.
- `tag` : (optional) Tag of container image. Default `latest`
- `path` : (required) Path to target application.
- `builder` : (required) Builder to use.
- `buildpacks` : (optional) URLs or Paths to Custom buildpacks, space separated.
- `env` : (optional) Environment variables, space separated.

> See "[Cloud Native Buildpack Documentation · Environment variables](https://buildpacks.io/docs/app-developer-guide/environment-variables/)" for environment valiables.


Example of building with buildpack

```yaml
on: [push]
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2

    - name: Build image
      uses: bigloupe/buildpacks-action@master
      with:
        image: 'sample-java-maven-app'
        path: 'samples/apps/java-maven/'
        builder: 'cnbs/sample-builder:alpine'
        buildpacks: 'samples/buildpacks/java-maven samples/buildpacks/hello-processes/ cnbs/sample-package:hello-universe'
```

## Available Builders 

Following builders are available in :

-	`Builder Google`:                `gcr.io/buildpacks/builder:v1`    -  Ubuntu 18 base image with buildpacks for .NET, Go, Java, Node.js, and Python                                              
-	`Builder Heroku stack 18`:                `heroku/buildpacks:18`    -          Base builder for Heroku-18 stack, based on ubuntu:18.04 base image                                                        
-	`Builder Heroku stack 20`:                `heroku/buildpacks:20`     -         Base builder for Heroku-20 stack, based on ubuntu:20.04 base image                                                        
-	`Paketo Buildpacks Base image ubuntu`:     `paketobuildpacks/builder:base` -    Ubuntu bionic base image with buildpacks for Java, .NET Core, NodeJS, Go, Ruby, NGINX and Procfile                        
-	`Paketo Buildpacks full image ubuntu`:     `paketobuildpacks/builder:full`  -   Ubuntu bionic base image with buildpacks for Java, .NET Core, NodeJS, Go, PHP, Ruby, Apache HTTPD, NGINX and Procfile     
-	`Paketo Buildpacks small image ubuntu`:     `paketobuildpacks/builder:tiny`  -   Tiny base image (bionic build image, distroless-like run image) with buildpacks for Java Native Image and Go
