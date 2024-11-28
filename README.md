# Daparm Vmware Collection

This repository contains the `daparm.vmware` Ansible Collection.

The collection is intended as a meta collection to have a single pane of glass over the various available vmware ansible content out there. Furthermore it should be used as customization over the already very advanced cloud.vmware_ops collection, to ensure a higher level of operational security.   
There will be a not to be neglected tradeoff between speed and ease of usage, because we basically transfer the reviewed and understood content of cloud.vmware_ops in this collection and add argument_specs to enforce only validated input.  

## External requirements

| Collection | Description | Python Dependencies | Ansible Dependencies | Link |
|----------|----------|----------|----------|----------|
| vmware.vmware | The vmware.vmware collection is part of the Red Hat Ansible Certified Content for VMware offering that brings Ansible automation to VMware. This collection brings forward the possibility to manage vSphere resources and automate operator tasks. | [`Pyvmomi`](https://github.com/vmware/pyvmomi) and [`vSphere Automation SDK for Python`](https://github.com/vmware/vsphere-automation-sdk-python) | - | [GitHub](https://github.com/ansible-collections/vmware.vmware) and [Redhat](https://console.redhat.com/ansible/automation-hub/repo/published/vmware/vmware/) |
| community.vmware | This repo hosts the community.vmware Ansible Collection.The collection includes the VMware modules and plugins supported by Ansible VMware community to help the management of VMware infrastructure. | [`pyvmomi`](https://pypi.org/project/pyvmomi/) >=8.0.3.0.1, [`vmware-vcenter`](https://pypi.org/project/vmware-vcenter/) and [`vmware-vapi-common-client`](https://pypi.org/project/vmware-vapi-common-client/) | [`vmware.vmware`](https://github.com/ansible-collections/vmware.vmware/) | [GitHub](https://github.com/ansible-collections/community.vmware) |
| vmware.vmware_rest | The vmware.vmware_rest collection is part of the Red Hat Ansible Certified Content for VMware offering that brings Ansible automation to VMware. This collection brings forward the possibility to manage vSphere resources and automate operator tasks. | [`Pyvmomi`](https://github.com/vmware/pyvmomi), [`vSphere Automation SDK for Python`](https://github.com/vmware/vsphere-automation-sdk-python) | [`cloud.common`](https://github.com/ansible-collections/cloud.common/) | [GitHub](https://github.com/ansible-collections/vmware.vmware_rest) and [Redhat](https://console.redhat.com/ansible/automation-hub/repo/published/vmware/vmware_rest/) |
| cloud.vmware_ops | This repository hosts the cloud.vmware_ops validated Ansible Collection. The collection includes a variety of Ansible roles and playbooks to help automate the management of VMware. It focuses on playbooks and roles that allow users to quickly and easily perform VMware operations tasks. The playbooks cover common use cases and leverage the roles inside the collection. The roles can be used to create your own playbooks and cover custom use cases for your environment. | [`Pyvmomi`](https://github.com/vmware/pyvmomi), [`vSphere Automation SDK for Python`](https://github.com/vmware/vsphere-automation-sdk-python) and [`aiohttp`](https://pypi.org/project/aiohttp/) | [`vmware.vmware_rest`](https://github.com/ansible-collections/vmware.vmware_rest)/[`vmware.vmware`](https://github.com/ansible-collections/vmware.vmware/)/[`community.vmware`](https://github.com/ansible-collections/community.vmware/)/[`community.general`](https://github.com/ansible-collections/community.general/)/[`ansible.posix`](https://github.com/ansible-collections/ansible.posix/)/[`cloud.common`](https://github.com/ansible-collections/cloud.common/) | [GitHub](https://github.com/ansible-collections/vmware.vmware) and [Redhat](https://console.redhat.com/ansible/automation-hub/repo/published/vmware/vmware/) |

### Install python requirements via pip

```bash
pip install -r requirements.txt
```

### Install ansible collection requirements via ansible-galaxy

#### Online from git

```bash
ansible-galaxy collection install git+https://github.com/daparm/daparm.vmware.git
```

#### Online via RedHat Automation Hub

To consume this Validated Content from Automation Hub, please ensure that you add the following lines to your ansible.cfg file.

```ini
[galaxy]
server_list = validated

[galaxy_server.validated]
url=https://console.redhat.com/api/automation-hub/content/validated/
auth_url=https://sso.redhat.com/auth/realms/redhat-external/protocol/openid-connect/token
token=<SuperSecretToken>
```

The token can be obtained from the [Automation Hub Web UI](https://console.redhat.com/ansible/automation-hub/token).

#### Offline via Private Automation Hub

``ìni
[galaxy]
server_list = automation_hub_pub,automation_hub_cert,automation_hub_validated,automation_hub_comm
ignore_certs = yes

[galaxy_server.automation_hub_cert]
url=https://<PRIVATE_HUB_URL>/api/galaxy/content/rh-certified/
token=<SuperSecretToken>

[galaxy_server.automation_hub_pub]
url=https://<PRIVATE_HUB_URL>/api/galaxy/content/published/
token=<SuperSecretToken>

[galaxy_server.automation_hub_comm]
url=https://<PRIVATE_HUB_URL>/api/galaxy/content/community/
token=<SuperSecretToken>

[galaxy_server.automation_hub_validated]
url=https://<PRIVATE_HUB_URL>/api/galaxy/content/validated/
token=<SuperSecretToken>
```

### vSphere compatibility

This collection supports vSphere 7.x and 8.x.

## Included content

<!--start collection content-->



<!--end collection content-->

## Using this collection

```bash
    ansible-galaxy collection install daparm.vmware
```

You can also include it in a `requirements.yml` file and install it via `ansible-galaxy collection install -r requirements.yml` using the format:

```yaml
collections:
  - name: daparm.vmware
```

To upgrade the collection to the latest available version, run the following command:

```bash
ansible-galaxy collection install daparm.vmware --upgrade
```

You can also install a specific version of the collection, for example, if you need to downgrade when something is broken in the latest version (please report an issue in this repository). Use the following syntax where `X.Y.Z` can be any [available version](https://galaxy.ansible.com/daparm/vmware):

```bash
ansible-galaxy collection install daparm.vmware:==X.Y.Z
```

See [Ansible Using collections](https://docs.ansible.com/ansible/latest/user_guide/collections_using.html) for more details.

## Release notes

See the [changelog](https://github.com/ansible-collections/daparm.vmware/tree/main/CHANGELOG.rst).

## Roadmap

<!-- Optional. Include the roadmap for this collection, and the proposed release/versioning strategy so users can anticipate the upgrade/update cycle. -->

## More information

<!-- List out where the user can find additional information, such as working group meeting times, slack/IRC channels, or documentation for the product this collection automates. At a minimum, link to: -->

- [Ansible Collection overview](https://github.com/ansible-collections/overview)
- [Ansible User guide](https://docs.ansible.com/ansible/devel/user_guide/index.html)
- [Ansible Developer guide](https://docs.ansible.com/ansible/devel/dev_guide/index.html)
- [Ansible Collections Checklist](https://github.com/ansible-collections/overview/blob/main/collection_requirements.rst)
- [Ansible Community code of conduct](https://docs.ansible.com/ansible/devel/community/code_of_conduct.html)
- [The Bullhorn (the Ansible Contributor newsletter)](https://docs.ansible.com/ansible/devel/community/communication.html#the-bullhorn)
- [News for Maintainers](https://github.com/ansible-collections/news-for-maintainers)

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
