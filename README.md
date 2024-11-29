# Daparm Vmware Ops Meta Collection

This repository contains the `daparm.vmware_ops_meta` Ansible Collection.

The collection is intended as a meta collection to have a single pane of glass over the various available vmware ansible content out there. Furthermore it should be used as customization over the already very advanced cloud.vmware_ops collection, to ensure a higher level of operational security.   
There will be a not to be neglected tradeoff between speed and ease of usage, because we basically transfer the reviewed and understood content of cloud.vmware_ops in this collection and add argument_specs to enforce only validated input.  

## Included content

<!--start collection content-->

As described, the collection will basicaly be a wrapper around the content of **cloud.vmware_ops**, so we'll mostly call the roles and playbooks from this collection, which already consumes the other existing ansible vmware content:

**vmware.vmware**, **vmware.vmware_rest** and **community.vmware**.  

### Overview of Collection "cloud.vmware_ops" - Version 1.6.0 

All existing roles - 13:  

| Name | Description |
| ----- | ----- |
| cluster_settings | Configure vCenter cluster settings |
| content_library | Manage a content library in vCenter |
| deploy_ovf | Deploy an OVF file as a VM on a vCenter or ESXi host |
| esxi_maintenance_mode | Manage an ESXi host's maintenance mode status |
| export_vm_as_ovf | Export a powered off VM on vCenter or an ESXi host as an OVF file |
| info | Gather info about vCenter guests, storage, license, cluster, or appliances |
| manage_folder | Manage a folder or folder path in vCenter |
| provision_vcenter | Deploy a vCenter appliance VM on an ESXi host using the VCSA ISO file |
| provision_virtual_esxi | Provision a virtual ESXi host VM on a vCenter or existing ESXi host |
| provision_vm | Provision a VM on vCenter or an ESXi host |
| snapshot_management | Manage a snapshot in vCenter |
| system_settings | Configure vCenter or ESXi system settings |
| vcenter_host_connection | Manage the connection of an ESXi host to a vCenter cluster |


All existing playbooks - 20:  


| Folder | Name | Description | Used Roles (FQCN) |
| ----- | ----- | ----- | ----- |
| cluster_settings | disable_high_availability.yml | Define cluster settings to disable HA | cloud.vmware_ops.cluster_settings |
| cluster_settings | enable_high_availability.yml | Define cluster settings to enable HA | cloud.vmware_ops.cluster_settings |
| cluster_settings | manage_all_settings.yml | Manages cluster settings | cloud.vmware_ops.cluster_settings |
| esxi_management | add_esxi_host_to_vcenter.yml | Add an ESXi host to a vCenter | cloud.vmware_ops.vcenter_host_connection |
| esxi_management | reconnect_esxi_host_in_vcenter.yml | Reconnect an ESXi host to a vCenter | cloud.vmware_ops.vcenter_host_connection |
| esxi_management | remove_esxi_host_in_vcenter.yml | Remove an ESXi host to a vCenter | cloud.vmware_ops.vcenter_host_connection |
| esxi_management | remove_esxi_host_in_vcenter.yml | Put an ESXi host In Maintenance Mode | cloud.vmware_ops.esxi_maintenance_mode |
| esxi_management | remove_esxi_host_in_vcenter.yml | Remove an ESXi host In Maintenance Mode | cloud.vmware_ops.esxi_maintenance_mode |
| provision_vcenter | provision_vcsa_on_esxi.yml | Provision a vCenter appliance on an ESXi host, using a vCenter ISO locally or VMX file on a datastore | cloud.vmware_ops.provision_vcenter |
| provision_vm | deploy_ovf.yml | Deploy a VM from an OVF file. The OVF can be located on the ansible_host filesystem, at a URL, or located in a content library | cloud.vmware_ops.deploy_ovf |
| provision_vm | manage_vm.yml | Provision a virtual machine and create associated resources if they don't exist (subnets, vCPU, memory configuration, storage configuration, etc). This includes cloning and building from VM templates | cloud.vmware_ops.provision_vm |
| snapshot_management | create_snapshot.yml | Create snapshot(s) of the given virtual machine | cloud.vmware_ops.snapshot_management |
| snapshot_management | remove_all_snapshots.yml | Remove all snapshot(s) of the given virtual machine | cloud.vmware_ops.snapshot_management |
| snapshot_management | remove_snapshots.yml | Remove snapshot(s) of the given virtual machine | cloud.vmware_ops.snapshot_management |
| snapshot_management | revert_to_a_snapshots.yml | Revert to a snapshot of the given virtual machine | cloud.vmware_ops.snapshot_management |
| ./ | export_vm_as_ovf.yml | export a VM from vCenter or ESXi as an OVF. The VM is exported to the local filesystem of the host running the tasks (ansible_host) | cloud.vmware_ops.export_vm_as_ovf |
| ./ | info.yml | Gathers information from vCenter | cloud.vmware_ops.info |
| ./ | manage_content_library.yml | manage VMWare content libraries. You can create or delete both local and subscribed content libraries | cloud.vmware_ops.content_library |
| ./ | manage_folder.yml | Manage folder or folder tree in vCenter | cloud.vmware_ops.manage_folder |
| ./ | system_settings.yml | define system settings for vCenter | cloud.vmware_ops.system_settings |


Currently we have high interest in the provisioning and the info functionality of the vmware_ops collection.  
The information gathering can be extended to a more advanced capacity planning needs and for templating the argument_specs.yml to reduce the manual overhead of creating VMWare resources and adding them back to the meta provision role for the sake of quality and security insurance.  

The provisioning part itself, only get's further restricted via an additional **meta/argument_specs.yml** file to provide a curated list of valid inputs.  
Visit [docs](./docs/adding_argument_specs.md)


## External requirements

| Collection | Description | Python Dependencies | Ansible Dependencies | Link |
|----------|----------|----------|----------|----------|
| vmware.vmware | The vmware.vmware collection is part of the Red Hat Ansible Certified Content for VMware offering that brings Ansible automation to VMware. This collection brings forward the possibility to manage vSphere resources and automate operator tasks. | [`Pyvmomi`](https://github.com/vmware/pyvmomi) and [`vSphere Automation SDK for Python`](https://github.com/vmware/vsphere-automation-sdk-python) | - | [GitHub](https://github.com/ansible-collections/vmware.vmware) and [Redhat](https://console.redhat.com/ansible/automation-hub/repo/published/vmware/vmware/) |
| community.vmware | This repo hosts the community.vmware Ansible Collection.The collection includes the VMware modules and plugins supported by Ansible VMware community to help the management of VMware infrastructure. | [`pyvmomi`](https://pypi.org/project/pyvmomi/) >=8.0.3.0.1, [`vmware-vcenter`](https://pypi.org/project/vmware-vcenter/) and [`vmware-vapi-common-client`](https://pypi.org/project/vmware-vapi-common-client/) | [`vmware.vmware`](https://github.com/ansible-collections/vmware.vmware/) | [GitHub](https://github.com/ansible-collections/community.vmware) |
| vmware.vmware_rest | The vmware.vmware_rest collection is part of the Red Hat Ansible Certified Content for VMware offering that brings Ansible automation to VMware. This collection brings forward the possibility to manage vSphere resources and automate operator tasks. | [`Pyvmomi`](https://github.com/vmware/pyvmomi), [`vSphere Automation SDK for Python`](https://github.com/vmware/vsphere-automation-sdk-python) | [`cloud.common`](https://github.com/ansible-collections/cloud.common/) | [GitHub](https://github.com/ansible-collections/vmware.vmware_rest) and [Redhat](https://console.redhat.com/ansible/automation-hub/repo/published/vmware/vmware_rest/) |
| cloud.vmware_ops | This repository hosts the cloud.vmware_ops validated Ansible Collection. The collection includes a variety of Ansible roles and playbooks to help automate the management of VMware. It focuses on playbooks and roles that allow users to quickly and easily perform VMware operations tasks. The playbooks cover common use cases and leverage the roles inside the collection. The roles can be used to create your own playbooks and cover custom use cases for your environment. | [`Pyvmomi`](https://github.com/vmware/pyvmomi), [`vSphere Automation SDK for Python`](https://github.com/vmware/vsphere-automation-sdk-python) and [`aiohttp`](https://pypi.org/project/aiohttp/) | [`vmware.vmware_rest`](https://github.com/ansible-collections/vmware.vmware_rest)/[`vmware.vmware`](https://github.com/ansible-collections/vmware.vmware/)/[`community.vmware`](https://github.com/ansible-collections/community.vmware/)/[`community.general`](https://github.com/ansible-collections/community.general/)/[`ansible.posix`](https://github.com/ansible-collections/ansible.posix/)/[`cloud.common`](https://github.com/ansible-collections/cloud.common/) | [GitHub](https://github.com/ansible-collections/vmware.vmware) and [Redhat](https://console.redhat.com/ansible/automation-hub/repo/published/vmware/vmware/) |

### vSphere compatibility

This collection supports vSphere 7.x and 8.x.

### Install python requirements via pip

```bash
pip install -r requirements.txt
```

### Install ansible collection requirements via ansible-galaxy

Ensure you can resolve the dependencies and prepare your ansible.cfg

#### Online via RedHat Automation Hub

To consume this Validated and Certified (published) Content from Automation Hub, please ensure that you add the following lines to your ansible.cfg file.

```ini
[galaxy]
server_list = validated, published, community

[galaxy_server.validated]
url=https://console.redhat.com/api/automation-hub/content/validated/
auth_url=https://sso.redhat.com/auth/realms/redhat-external/protocol/openid-connect/token
token=<SuperSecretToken>

[galaxy_server.published]
url=https://console.redhat.com/api/automation-hub/content/published/
auth_url=https://sso.redhat.com/auth/realms/redhat-external/protocol/openid-connect/token
token=<SuperSecretToken>

[galaxy_server.community]
url=https://galaxy.ansible.com/
```

The token can be obtained from the [Automation Hub Web UI](https://console.redhat.com/ansible/automation-hub/token).

#### Offline via Private Automation Hub

To download the content from a private automation hub, create this ansible.cfg

```ini
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

The token can be obtained from the [Private Automation Hub Web UI](https://<PRIVATE_HUB_URL>/content/api-token).

#### From git resource

```bash
ansible-galaxy collection install git+https://github.com/daparm/daparm.vmware_ops_meta.git
```

If ansible.cfg points to an Private Automation Hub you can omit the git+prefix

```bash
    ansible-galaxy collection install daparm.vmware_ops_meta
```

You can also include it in a `requirements.yml` file and install it via `ansible-galaxy collection install -r requirements.yml` using the format:

```yaml
collections:
  - name: daparm.vmware_ops_meta
```

To upgrade the collection to the latest available version, run the following command:

```bash
ansible-galaxy collection install daparm.vmware_ops_meta --upgrade
```

You can also install a specific version of the collection, for example, if you need to downgrade when something is broken in the latest version (please report an issue in this repository). Use the following syntax where `X.Y.Z` can be any [available version](https://github.com/daparm/daparm.vmware_ops_meta.git):

```bash
ansible-galaxy collection install daparm.vmware_ops_meta:==X.Y.Z
```

## Release notes

See the [changelog](https://github.com/ansible-collections/daparm.vmware_ops_meta/tree/main/CHANGELOG.rst).

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
