# build-go

go-build is a reusable container for building Go projects that use gb. In an
effort to standardize the build process, it makes a few simple of assumptions.

* You are using gb.
* You have all of your vendor packages already.
* You require that all tests be passing in order to build.
* You may have additional build steps unique to a project.

## Building with build-go

NOTE: until we move to Go 1.5, we do not support cross-compilation so specifying TARGETS won't
do you any good. We're only compiling to linux/amd64 at the moment.

```
docker pull quay.io/opsee/build-go
docker run --rm -v $(pwd):/build -e "TARGETS=linux/amd64 darwin/amd64" quay.io/opsee/build-go
```

Resulting binaries and packages will end up in:

* target/
  * linux/
    * x86_64/
      * bin/
      * pkg/
  * darwin/
    * x86_64/
      * bin/
      * pkg/

## Local build.sh

You may place a build.sh file in the root of your project for additional build steps. It will be run before the `gb build`.
