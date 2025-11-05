# ACCESS-ESM1.5: ACCESS Earth System Model

## About the model

The ACCESS Earth System Model (ACCESS-ESM) is a fully-coupled global climate model that includes atmoshpere, land, ocean, sea ice, ocean biogeochemistry and land biogeochemistry components, linked together by a coupler.

ACCESS-ESM1.5 was developed by CSIRO (Ziehn T, Chamberlain MA, Law RM, Lenton A, Bodman RW, Dix M, Stevens L, Wang YP, Srbinovsky J, 2020: The Australian Earth System Model: ACCESS-ESM1.5. Journal of Southern Hemisphere Earth Systems Science 70 , 193–214, https://doi.org/10.1071/ES19035)

Details about the model components is available on the ACCESS Hive Docs:

https://docs.access-hive.org.au/models/access_models/access-esm/

And instructions for how to run the model:

https://docs.access-hive.org.au/models/run_a_model/run_access-esm/

## Support

[ACCESS-NRI](https://www.access-nri.org.au) has assumed responsibility for supporting ACCESS-ESM1.5 for the Australian Research Community. As part of this support ACCESS-NRI has developed a new build and deployment system for ACCESS-ESM1.5 to align with plans for supporting a range of Earth System Models.

Any questions about ACCESS-NRI releases of ACCESS-ESM1.5 should be done through the [ACCESS-Hive Forum](https://forum.access-hive.org.au/). See the [ACCESS Help and Support topic](https://forum.access-hive.org.au/t/access-help-and-support/908) for details on how to do this.

### Build

ACCESS-NRI is using [spack](https://spack.io), a build from source package manager designed for use with high performance computing. This repository contains a [spack environment](https://spack.readthedocs.io/en/latest/environments.html) definition file ([`spack.yaml`](https://github.com/ACCESS-NRI/ACCESS-ESM1.5/blob/main/spack.yaml)) that defines all the essential components of the ACCESS-ESM1.5 model, including exact versions.

Spack automatically builds all the components and their dependencies, producing model component executables. Spack already contains support for compiling thousands of common software packages. Spack packages for the components in ACCESS-ESM1.5 are defined in the [spack packages repository](https://github.com/ACCESS-NRI/spack_packages/).

ACCESS-ESM1.5 is built and deployed automatically to `gadi` on NCI (see below). However it is possible to use spack to compile the model using the `spack.yaml` environment file in this repository. To do so follow the [instructions on the ACCESS Forum for configuring spack on `gadi`](https://forum.access-hive.org.au/t/how-to-build-access-om2-on-gadi/1545).

Then clone this repository and run the following commands on `gadi`:

```bash
spack env create access-esm1p5 spack.yaml
spack env activate access-esm1p5
spack install
```

to create a spack environment called `access-esm1p5` and build all the models components, the locations of which can be found using `spack find --paths`.

### Deployment

ACCESS-ESM1.5 is deployed automatically when a new version of the [`spack.yaml`](https://github.com/ACCESS-NRI/ACCESS-ESM1.5/blob/main/spack.yaml) file is committed to `main` or a dedicated `backport/VERSION` branch. All the ACCESS-ESM1.5 components are built using `spack` on `gadi` and installed under the [`vk83`](https://my.nci.org.au/mancini/project/vk83) project in `/g/data/vk83`. It is necessary to be a member of [`vk83`](https://my.nci.org.au/mancini/project/vk83) project to use ACCESS-NRI deployments of ACCESS-ESM1.5.

The deployment process also creates a GitHub release with the same tag. All releases are available under the [Releases page](https://github.com/ACCESS-NRI/ACCESS-ESM1.5/releases). Each release has a changelog and meta-data with detailed information about the build and deployment, including:

- paths on `gadi` to all executables built in the deployment process (`spack.location`)
- a `spack.lock` file, which is a complete build provenance document, listing all the components that were built and their dependencies, versions, compiler version, build flags and build architecture
- the environment `spack.yaml` file used for deployment

Additionally the deployment creates environment modulefiles, the [standard method for deploying software on `gadi`](https://opus.nci.org.au/display/Help/Environment+Modules). To view available ACCESS-ESM1.5 versions:

```bash
module use /g/data/vk83/modules
module avail access-esm1p5
```

For users of ACCESS-ESM1.5 model configurations released by ACCESS-NRI the exact location of the ACCESS-ESM1.5 model executables is not required. Model configurations will be updated with new model components when necessary.

For information on contributing your own fixes to the ACCESS-ESM1.5 `spack.yaml`, see the [CONTRIBUTING.md](./CONTRIBUTING.md) file.
