# HOW TO BUILD JikesRVM
## Follow the Instructions to build a development environment for [JikesRVM](https://github.com/mmtk/mmtk-jikesrvm).

1. Install Docker on your device.
2. Open the terminal.
3. Clone this repo.

```
$ cd path/to/repo

$ docker build -t name_of_image .        # build an image, replace the name by anything
$ docker run --name name_of_container -it name_of_image /bin/bash      # run the image in an new container, give it a name

$ git clone https://github.com/JikesRVM/JikesRVM.git              # clone JikesRVM's repository
$ cd jikesrvm

$ update-alternatives --config java      # change jdk version to jdk 8
Press <enter> to keep the current choice[*], or type selection number: q
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      manual mode
  2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode

Press <enter> to keep the current choice[*], or type selection number: 2

$ bin/buildit localhost development     # now build
```
Now you should have built JikesRVM, use the same container everytime.
```
$ docker exec -it name_of_container /bin/bash     # Start a stopped container.
```
## MMTk Dependencies

This repo provides a docker file which lists the dependencies of [MMTk](https://github.com/mmtk/mmtk-core) and its bindings for [V8](https://github.com/mmtk/mmtk-v8), [OpenJDK](https://github.com/mmtk/mmtk-openjdk) and [JikesRVM](https://github.com/mmtk/mmtk-jikesrvm).

This docker file is based-on the official _Ubuntu-18.04_ (bionic) docker image which can be found [here](https://hub.docker.com/_/ubuntu).
As the docker is minimal, the docker file may install packages (such as `locales`) which are already included on a standard Ubuntu-18.04 installation.

Unless stated otherwise in the dockerfile, package versions are the latest installable through the `apt-get` command on _Ubuntu-18.04_.

## Software Dependencies

Currently, the MMTk team run the development and testing of MMTk and bindings on Ubuntu-18.04.

As in [Dockerfile](https://github.com/mmtk/mmtk-dev-env/blob/main/Dockerfile), setting up the dependencies can be done through these steps:

1. Install the required packages: [Dockerfile#17](https://github.com/mmtk/mmtk-dev-env/blob/main/Dockerfile#L17),
2. Install `rustup` and add it to `PATH`: [Dockerfile#20-21](https://github.com/mmtk/mmtk-dev-env/blob/main/Dockerfile#L20-L21),
3. Install our currently used nightly Rust toolchain using `rustup`: [Dockerfile#25](https://github.com/mmtk/mmtk-dev-env/blob/main/Dockerfile#L25),
4. Add the `i686-unknown-linux-gnu` target to the Rust toolchain: [Dockerfile#26](https://github.com/mmtk/mmtk-dev-env/blob/main/Dockerfile#L26)

__NOTE:__ We successfully tried the same procedure on Ubuntu-20.04, but Ubuntu-18.04 is still the version we use daily.
