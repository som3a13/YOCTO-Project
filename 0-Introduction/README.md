# Yocto Project

The Yocto Project is an open-source collaboration project that provides tools and resources for creating custom Linux distributions for embedded systems. It offers a flexible framework for building embedded Linux systems, allowing developers to customize their distributions to meet specific requirements. Yocto streamlines the development process by providing tools for package management, configuration, and cross-compilation.

Output: Linux Based Embedded Product
*(Linux Kernel, Root File System, Bootloader, Device Tree, Toolchain)

#### Why to use Yocto?

* To configure the Linux according to our specs.
* The Image contains what we need.
* No extra packages.
* Small Image Size.

# What is Poky?

**Poky** is a reference distribution of the Yocto Project.It serves as a starting point for developers to create their own customLinux distribution. Poky includes the Yocto Project's core metadata, apre-configured build environment, and a default build configuration. It is essentially a ready-to-start toolkit for building Yocto-based distributions and includes everything required to run the BitBake tool and to bootstrap a basic embedded Linux image. Poky integrates the OpenEmbedded-Core metadata, a kernel, and a bootloader, among other components.

# What is BitBake?

**BitBake** is a task executor and scheduler written in Python. It is used extensively by the Yocto Project as its core build engine. BitBake interprets metadata (written in a special format that includes Python scripting), organizes the dependencies, and executes tasks according to specified dependencies and priorities. This tool handles the downloading and unpacking of source code, the configuration and compilation of that code, and the packaging of the resulting binaries in an efficient and coherent manner.

# Recipes

**Recipes** are detailed instructions used by the Yocto Project to build specific software packages. Each recipe includes:

* **Source location** : URL to download the software source.
* **Dependencies** : Other packages needed.
* **Configuration options** : Specific setup instructions.
* **Patching** : Modifications applied to the source.
* **Compilation and installation instructions** : Steps to build and install the package.

# Meta-layers

**Meta-layers** are collections of recipes and configuration files that organize and modularize components in a Yocto Project. They allow:

* **Organization** : Groups related recipes for clarity.
* **Modularity** : Enables adding or removing feature sets easily.
* **Customization** : Facilitates user-specific adjustments without altering core recipes.

These elements help structure and streamline the process of creating custom Linux distributions for embedded systems.

### Overview of Components

1. **BitBake** : This is the build tool at the heart of the Yocto Project. It interprets metadata (mostly written in recipes), resolves dependencies, and executes tasks such as compiling and configuring software.
2. **Recipes** : These are instructions for building a particular piece of software. They include details such as where to download the source, how to configure and compile it, any patches that need to be applied, and dependencies on other recipes.
3. **Configuration Files** : These are primarily found in the `conf` directory of your Yocto build environment. Important configuration files include:

* `bblayers.conf`: Lists all the meta-layers that BitBake should consider during the build.
* `local.conf`: Contains local configuration settings such as machine type, number of parallel jobs for BitBake, and other specific build options.

1. **Meta-layers** : Organizational units in Yocto that group together recipes and configuration data related to specific components or functionalities.

### How They Work Together

1. **Initialization** : When setting up a Yocto build, you first source an environment setup script (`oe-init-build-env`). This script prepares the environment, setting up necessary variables and pointing to the build directory where `conf/bblayers.conf` and `conf/local.conf` are located.
2. **Configuration Setup** :

* `bblayers.conf` is configured to include your custom layers along with the standard Yocto layers.
* `local.conf` is customized for specific build parameters like hardware architecture.

1. **Building with BitBake** : You invoke BitBake along with a target recipe, e.g., `bitbake core-image-minimal`. BitBake processes the instructions in the specified recipes:

* It fetches the source code.
* Applies necessary patches.
* Compiles the source.
* Packages the software into an installable format.
* Finally, assembles all packages into a complete image.
