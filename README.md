# tier34 repo

A repository that includes YAML manifests. Manifests can define GCP resources in `config connector` format or the Kubernetes components and resources. Refer to this repo for additionnal information. TODO: add link

## csync

The `/csync` contains the configuration for what the ConfigSync operator should be observing. For example, It is within this configuration that you specify the `repo url`, the `folder`, the `branch` and the `tag`.

Contributing:

- Any modification should be implemented within the `source-customization` folder.

Permissions:

- A pull request affecting `/csync/source-customization/dev/*/setters-version.yaml` will include the Application Developer as required reviewers.
- A pull request affecting `/csync/source-customization/preprod/*/setters-version.yaml` will include the Application Operator as required reviewers.
- A pull request affecting `/csync/source-customization/prod/*/setters-version.yaml` will include the Application Operator as required reviewers.
- A pull request affecting any other file under `/csync` will include the Security Admin and the Platform admin as required reviewers.

## tier3

The `/tier3` folder is where security and networking resources that enables the applications are defined.

Contributing:

- Any modification should be implemented within the `source-customization` folder.

Permissions:

- A pull request affecting this folder will include the Security Admin and the Platform admin as required reviewers.

## tier4

The `/tier4` folder is where application resources that have to be provisionned in the GCP project are defined.

Contributing:

- The `/tier4/deploy/<env>` folders are the only required folders. These are observed by the configsync operator. Besides those folders, contributors can decide on the folder structure and content underneath that folder.

- Developers may want to consider using customization tools to modify the infrastructure for each environment. To achieve that, the `/csync` and the `/tier3` folders are using a combination of `KPT` packages and the script `/tools/scripts/kpt/hydrate.sh`. That same solution can be re-used under the `/tier4` folder if KPT packages is chosen to be the customization solution.

  Other options to consider are [Helm Charts](https://helm.sh/) and [Kustomize](https://kustomize.io/).

Permissions:

- A pull request affecting `/tier4/deploy/dev` will include the Application Developer as required reviewers.
- A pull request affecting `/tier4/deploy/preprod` will include the Application Operator as required reviewers.
- A pull request affecting `/tier4/deploy/prod` will include the Application Operator as required reviewers.
- A pull request affecting any other file under `/tier4` will include the Application Developer as required reviewers.

## Tags

Tags are generated only when changes are affecting the `/tier3` or the `/tier4` folders. This functionality is possible because of the `version-tagging` pipeline.

The tags will be created by that pipeline job after commits are merge to the `main` branch.

### **IMPORTANT**

We recommend using those tags in the `setters-version.yaml` under the `/csync/source-customization` folder to define what has to be observed by the configsync operator.

## Branch Protection

The main branch of this repository is protected meaning that pushing new commit to it will be denied. To implement changes, A Pull Request has to be completed.

Every other branches configured to be observed by ConfigSync will also have a a branch protection rule defined.
TODO: add more details
