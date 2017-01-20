---
title: Transfer Package

---


:::hint
Transfer a package was introduced in Octopus Deploy 3.7.12
:::

## Transferring a package to your target without extraction


If you just want to transfer a package to your remote target without extracting or processing its contents like the standard [Deploy a package](/docs/home/deploying-applications/deploying-packages.md) step, then you will want to use the Transfer a package step. When adding this step to your deployment process, choose the **Transfer a Package** option. For more information, see the [add step](http://docs.octopusdeploy.com/display/OD/Add+step) section.


![](/docs/images/5671696/5866194.png)


When transferring a package you will need to specify a location that the file will be copied to once it has been uploaded from the server. This can be either a hard-coded path, or a bound variable.


![](/docs/images/5672327/5866214.png)


This package will be transferred to the target during the package acquisition phase, and then copied to the specified location at the appropriate time during the deployment process. The copy process is used as opposed to moving or simply transferring it directly to the requested location during acquisition for a number of reasons. First, this will allow the package location to be derived from output variables from previous steps while allowing the full acquisition process to occur up-front, and secondly it will allow the [delta compression](http://docs.octopusdeploy.com/display/OD/Delta+compression+for+package+transfers) checks to take place to reduce to amount of data that needs to be transferred on subsequent deployments.

## Output Variables


Since the Transfer a Package step has been kept simple by-design, most deployments will probably want to use the transferred package for some further processing. For this purpose, the following [output variables](/docs/home/deploying-applications/variables/output-variables.md) are generated for access by subsequent steps.

- `Octopus.Action[StepName].Output.Package.DirectoryPath`- The directory the package was transferred to
- `Octopus.Action[StepName].Output.Package.FileName` - The name of the package
- `Octopus.Action[StepName].Output.Package.FilePath`- The full path to the package



Note that once transferred the package file name will take the format of `&lt;PackageId&gt;.&lt;PackageName&gt;.&lt;FileExtension&gt;`however the expectation is that this should be the original filename to begin with.