# tier34 repo

A repository that includes YAML manifests. Manifests can define GCP resources in `config connector` format or the Kubernetes components and resources. Refer to this repo for additional information. TODO: add link

- The `/*/configcontroller` folder is where GCP resources are defined using their `config connector` schema.
- The `/*/kubernetes/_X-FLEET-ID/**/_NAMESPACE` folder is where resources that have to be provisioned in a kubernetes `namespace` are defined. The `_X-FLEET-ID` is the GCP project-id where the kubernetes clusters are deployed with character "x" as the environment code because this folder will contain the configuration for all environments.

  The GKE clusters are joined to an [Anthos Fleet](https://cloud.google.com/anthos/fleet-management/docs). This enables Anthos policy controller, Anthos config management and Anthos service mesh(future).

## csync

The `/csync` contains the configuration for what the ConfigSync operator should be observing. For example, It is within this configuration that you specify the `repo url`, the `folder`, the `branch` and the `tag`.

### Contributing

- Any modification should be implemented within the `source-customization` folder.

### Permissions

- A pull request affecting `/csync/**/source-customization/dev/*/setters-version.yaml` will include the Application Developer as required reviewers.
- A pull request affecting `/csync/**/source-customization/preprod/*/setters-version.yaml` will include the Application Operator as required reviewers.
- A pull request affecting `/csync/**/source-customization/prod/*/setters-version.yaml` will include the Application Operator as required reviewers.
- A pull request affecting any other file under `/csync` will include the Security Admin and the Platform admin as required reviewers.

## tier3

The `/tier3` folder is where security and networking resources that enables the applications are defined.

### Contributing

- Any modification should be implemented within the `source-customization` folder.

### Permissions

- A pull request affecting this folder will include the Security Admin and the Platform admin as required reviewers.

## tier4

- The `/tier4/architecture` folder is where you can store **design** documents describing your application. These will be reviewed by the security admins and the platform admins when you will submit a pull request affecting `tier3`.
- The `/tier4/configcontroller` folder is where application resources that have to be provisioned in the GCP project are defined.
- The `/tier4/kubernetes/_X-FLEET-ID/**/_NAMESPACE` folder is where resources that have to be provisioned in a kubernetes namespace are defined.

>> Replace `_X-FLEET-ID` with fleet-id and character "x" as the environment code because this folder will contain the configuration for all environments.

### Contributing

- The `/tier4/**/deploy/<env>` folders are the only required folders. These are observed by the configsync operator. Besides those folders, contributors can decide on the folder structure and content underneath that folder.

- Developers may want to consider using customization tools to modify the infrastructure for each environment. To achieve that, the `/csync` and the `/tier3` folders are using a combination of `KPT` packages and the script `/tools/scripts/kpt/hydrate.sh`. That same solution can be re-used under the `/tier4` folder if KPT packages is chosen to be the customization solution.

  Other options to consider are [Helm Charts](https://helm.sh/) and [Kustomize](https://kustomize.io/).

### Permissions

- A pull request affecting `/tier4/**/deploy/dev` will include the Application Developer as required reviewers.
- A pull request affecting `/tier4/**/deploy/preprod` will include the Application Operator as required reviewers.
- A pull request affecting `/tier4/**/deploy/prod` will include the Application Operator as required reviewers.
- A pull request affecting any other file under `/tier4` will include the Application Developer as required reviewers.

## Branch Protection

The main branch of this repository is protected meaning that pushing a new commit to it will be denied. To implement changes, A Pull Request has to be completed.

Every other branches configured to be observed by ConfigSync will also have a branch protection rule defined.
TODO: add more details
