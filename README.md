GitHub Action templates to support Keyfactor Integration Catalog and Release processes. Note that while this repository is publicly visible, its contents are intended
for Keyfactor internal use.

# Release Actions
The bootstrap workflow will checkout, setup, and build the Keyfactor extension automatically when a branch matching the release-[0-9]+\.[0-9]+ pattern.  The branch name is used to label the release in Github and determine the Major and Minor version. The release and source will be tagged automatically and the bump determined by the branch name's version e.g. `release-1.2` will build Major.Minor version 1.2. The Patch and pre-release version numbers will be auto-incremented as additional builds happen from that branch.

Addtionally, the workflow will automatically apply the generated tag version number to the .net assemblies prior to the build.  This ensures the tagged version number matches the file version.  If any step fails, the workflow will remove any release/tags created as part of the process. 


# Adding the Release Action to your Repo
All workflow YAML files must be located in the .github/workflows directory of your repository.  A file can be created manually and pushed to the repo or a new file copied from the Keyfactor template in the Actions > New Workflow menu option

Most of the template is ready to use and will dynamically find the solution file, the release name(from branch name), and the repository name used to artifacts. However, due to the variability in project structures and dependencies a few manual modifications will be required.

## TODO when adding a build template
* Update the integration-manifest.json

ca-gateways

    gateway_framework (ca-gateways only)

orchestrators

    about.orchestrator.UOFramework

    about.orchestrator.pam_support

PAM providers

    about.pam.AssemblyName

    about.pam.fullyQualifiedClassName

    about.pam.dbName

Required files All Integration Types

    readme_source.md

    integration-manifest.json

# Assumptions
* CHANGELOG.md must be located in the root of the repository.  The release process will create a link to this file from the release to document changes/release notes. 
* readme_source.md must be located in the root of the repository. This markdown is added to the generated sections of the readme from template.
* integration-manifest.json must be located in the root of the repository. Values from this json file will be used in the readme template andto control certain subtasks of the bootstrap workflow.
