# Variables for Yocto Project:

### Common Recipe Variables

#### 1. **PN (Package Name)**

* **Description** : Represents the name of the package being built.

#### 2. **PV (Package Version)**

* **Description** : Specifies the version of the package.

#### 3. **PR (Package Revision)**

* **Description** : Indicates the revision of the package, often used to denote package updates.

#### 4. **WORKDIR**

* **Description** : The working directory where BitBake compiles the package.

#### 5. **S (Source Directory)**

* **Description** : Directory where the source code of the package is unpacked and prepared for building.

#### 6. **D (Destination Directory)**

* **Description** : Directory used by BitBake as the staging area for installing files as if they are in the root filesystem.

#### 7. **B (Build Directory)**

* **Description** : Directory where the build occurs. It is used for compiling the package.

## How to Read Variable Value

```
bitbake -e <RECIPE_NAME> | grep ^<VARIABLE_NAME>=
```

## Variables for local.conf 

#### 1. **MACHINE**

* **Description** : Specifies the target hardware for the build.
* **Example** : `MACHINE = "raspberrypi3"`

#### 2. **DISTRO**

* **Description** : Determines which distribution settings to use.
* **Example** : `DISTRO = "poky"`

#### 3. **BB_NUMBER_THREADS**

* **Description** : Sets the number of parallel threads BitBake should use during task execution. Increasing this number can speed up the build process on multicore machines.
* **Example** : `BB_NUMBER_THREADS = "8"`

#### 4. **PARALLEL_MAKE**

* **Description** : Controls the number of make jobs to run concurrently during the compilation of individual packages. It's often set similar to the number of CPU cores available.
* **Example** : `PARALLEL_MAKE = "-j 8"`

#### 5. **DL_DIR**

* **Description** : Defines the directory where source code files (downloads) are stored.
* **Example** : `DL_DIR = "${TOPDIR}/downloads"`

#### 6. **SSTATE_DIR**

* **Description** : Specifies the shared state cache directory. Using shared state caches can significantly reduce build time by providing precompiled components.
* **Example** : `SSTATE_DIR = "${TOPDIR}/sstate-cache"`

#### 7. **TMPDIR**

* **Description** : Sets the directory used for storing temporary build files.
* **Example** : `TMPDIR = "${TOPDIR}/tmp"`

#### 8. **IMAGE_INSTALL_append**

* **Description** : Appends additional packages to be included in the final image. Always precede the package name with a space to avoid concatenation errors.
* **Example** : `IMAGE_INSTALL_append = " nano vim"`

#### 9. **INHERIT**

* **Description** : Specifies which classes to inherit in the build configuration. For example, `rm_work` class removes work directories after a recipe is built to save disk space.
* **Example** : `INHERIT = "rm_work"`

#### 10. **IMAGE_FEATURES**

* **Description** : Adds specific features to the built image, such as server capabilities, debugging tools, or graphical support.
* **Example** : `IMAGE_FEATURES += "ssh-server-dropbear"`

### Check Variables assignment for yocto variable documentations : [Variables assignment](https://docs.yoctoproject.org/bitbake/2.2/bitbake-user-manual/bitbake-user-manual-metadata.html)
