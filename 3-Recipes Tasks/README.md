# **Tasks in Recipes**

BitBake recipes define several tasks that are executed in a specific order to build the package. Here’s an overview of some common tasks you might encounter:

* **do_fetch** : Downloads the source code from the location specified in `SRC_URI`.
* **do_unpack** : Extracts the downloaded source into a working directory.
* **do_patch** : Applies any patches defined in the recipe.
* **do_configure** : Configures the source by setting up the makefiles and any necessary build configuration.
* **do_compile** : Compiles the source code into binaries.
* **do_install** : Installs the compiled binaries into a temporary directory structured like the target root filesystem.
* **do_package** : Splits the files in the temporary installation directory into individual packages.
* **do_build** : A pseudo-task that generally encompasses fetching, unpacking, patching, configuring, compiling, and installing.

if you want to run specifi task in recipe do :

```
bitbake -c do_<task> recipie-name
```

**Refrence** : [https://docs.yoctoproject.org/ref-manual/tasks.html]()

# Example Yocto Recipe Breakdown 

#### 1.Metadata

```
DESCRIPTION = "This is a simple Hello World  recipe - uses a fetched source code from github"
HOMEPAGE = "https://github.com/som3a13/.com"
LICENSE = "MIT"
LIC_FILES_CHKSUM = "file://${COMMON_LICENSE_DIR}/MIT;md5=0835ade698e0bcf8506ecda2f7b4f302"

```

* **DESCRIPTION** : Provides a brief description of the recipe's purpose.
* **HOMEPAGE** : Indicates the project's homepage for more information.
* **LICENSE** : Specifies the license under which the recipe and the software are distributed.
* **LIC_FILES_CHKSUM** : This is a checksum (md5 in this case) to verify the integrity of the license file. Ensures compliance with the recipe's stated license.

#### 2. **Source**

```bitbake
SRC_URI = "https://github.com/som3a13/Test2Fetch.git;protocol=https;branch=main"
SRCREV = "a1a9446cfa4eb0f9ed10e3c4e3221f9127c4a750"
S = "${WORKDIR}/git"
```

* **SRC_URI** : Defines the location of the source code. This recipe pulls from a GitHub repository. Note there's a typo in `protocol=https`.
* **SRCREV** : Specifies the exact commit to use, ensuring repeatable builds.
* **S** : Points to the directory where the source code is unpacked and built. By default, it’s set to the `git` directory inside the work directory (`${WORKDIR}`).

#### 3. **Inheritance**

```
inherit cmake

```

* **inherit** : This line tells BitBake to include functionality from another class. `cmake` is a class provided by Yocto that simplifies building with CMake.

#### 4. Functions

This functions **overrides** the work of the inherited cmake . That implementation only to practice on our do_tasks

```bitbake
do_configure() {
    echo "Configuring 'Hello, World!' application..."
    mkdir -p ${WORKDIR}/build
    cd ${WORKDIR}/build
    cmake ${S} -DCMAKE_INSTALL_PREFIX=${WORKDIR}
}
do_compile() {
    echo "Compiling 'Hello, World!' application..."
    cd ${WORKDIR}/build
    make
}
do_install() {
    cd ${WORKDIR}/build
    make install
    install -d ${D}${bindir}
    install -m 0755 HelloApp ${D}${bindir}

    #TO CHECK OUR WORK as i've enabled rm_work in my local.conf ^.^
    cp -r ${WORKDIR} ~/Desktop
}
```

* **do_configure** : Prepares the build directory and runs `cmake` with specified variables.
* **do_compile** : Compiles the source code using `make`.
* **do_install** : Installs the binaries into the designated directory within the image. {bindir is usr/bin}

**To Build our Recipe do :**

```
bitbake <recipe-name>
```

### Notes

* The `do_install` task includes a non-standard practice of copying the build directory to a developer's desktop. This might be useful for debugging but should be used cautiously, especially in shared or production environments.
* The recipe assumes the output binary from the build is `HelloApp`. Ensure this matches the actual target output from the make process.
