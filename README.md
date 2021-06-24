GitHub Action templates to support Keyfactor Integration Catalog and Release processes. Note that while this repository is publicly visible, its contents are intended
for Keyfactor internal use.

# Release
The release workflow will checkout, setup, and build the Keyfactor extension automatically when a branch matching the release-v[1-9]\.[0-9]+\.[0-9]+ pattern.  The branch name is used to label the release in Github.  The release and source will be tagged automatically and the bump determined by the auto_increment_type setting in the workflow (default patch). The action will find the last tag (if it exists) and increment by one; otherwise, it will begin numbering at 1.0.0

Addtionally, the workflow will automatically apply the generated tag version number to the .net assemblies prior to the build.  This ensures the tagged version number matches the file version.  If any step fails, the workflow will remove any release/tags created as part of the process. 

# Adding the Action to your Repo
All workflow YAML files must be located in the .github/workflows directory of your repository.  A file can be created manually and pushed to the repo or a new file copied from the Keyfactor template in the Actions > New Workflow menu option

Most of the template is ready to use and will dynamically find the solution file, the release name(from branch name), and the repository name used to artifacts. However, due to the variability in project structures and dependencies a few manual modifications will be required.
* Change Compress-Archive command in the Archive Files step to match the expected release output
* Update the auto_increment_type to match the version numbering you want (major, minor, or patch level bump)

# Assumptions
* CHANGELOG.md must be located in the root of the repository.  The release process will create a link to this file from the release to document changes/release notes. 
