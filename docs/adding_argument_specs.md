#### Manual Workflow importing a role from upstream to our meta collection:

```bash
mkdir tmp_work_dir
cd $_
git init
git remote add origin -f https://github.com/redhat-cop/cloud.vmware_ops.git
git pull origin main
mv roles/provision_vm roles/deploy_ovf/ roles/info/ ../roles/
cd -
rm -rf tmp_work_dir
```

Adding a meta/argument_specs.yml file to the provision_vm role:  

```bash
cat <<EOF> roles/provision_vm/meta/argument_specs.yml
---
argument_specs:
  main:
    short_description: Provision a VM in VMware vSphere
    description:
      - A role to provision a virtual machine and create associated resources if they don't exist (subnets, vCPU, memory configuration, storage configuration, etc). 
      - This includes cloning and building from VM templates.
    options:

    ### General Authentication Role Variables
      provision_vm_hostname:
        description:
          - The hostname or IP address of the vSphere vCenter or ESXi host.
          - If this variable is not set, the collection level variable vmware_ops_hostname will be used. If that variable is not set, the environment variable VMWARE_HOST will be used. At least one of these variables must be set to use this role.
        type: str
        required: true

      provision_vm_username:
        description:
          - The vSphere vCenter or ESXi host username.
          - If this variable is not set, the collection level variable vmware_ops_username will be used. If that variable is not set, the environment variable VMWARE_USER will be used. At least one of these variables must be set to use this role.
        type: str
        required: true

      provision_vm_password:
        description:
          - The vSphere vCenter or ESXi host password.
          - If this variable is not set, the collection level variable vmware_ops_password will be used. If that variable is not set, the environment variable VMWARE_PASSWORD will be used. At least one of these variables must be set to use this role.
        type: str
        required: true

      provision_vm_validate_certs:
        description:
          - Allows connection when SSL certificates are not valid. Set to false when certificates are not trusted.
          - If this variable is not set, the collection level variable vmware_ops_validate_certs will be used. If that variable is not set, the environment variable VMWARE_VALIDATE_CERTS will be used.
        type: bool
        required: false

      provision_vm_port:
        description:
          - The port used to authenticate to the vSphere vCenter or ESXi host.
          - If this variable is not set, the collection level variable vmware_ops_port will be used. If that variable is not set, the environment variable VMWARE_PORT will be used.
        type: int
        required: false

    ### General Proxy Role Variables

      provision_vm_proxy_host:
        description:
          - The hostname of a proxy host that should be used for all HTTPs communication by the role.
          - The format is a hostname or an IP.
          - If this variable is not set, the collection level variable vmware_ops_proxy_host will be used. If that variable is not set, the environment variable VMWARE_PROXY_HOST will be used.
        type: str
        required: false

      provision_vm_proxy_port:
        description:
          - The port of a proxy host that should be used for all HTTPs communication by the role
          - If this variable is not set, the collection level variable vmware_ops_proxy_host will be used. If that variable is not set, the environment variable VMWARE_PROXY_PORT will be used.
        type: int
        required: false

    ### Specific Role Variables

      provision_vm_name:
        description:
          - Name of the virtual machine to manage.
          - Virtual machine names in vCenter are not necessarily unique which may be problematic. If multiple virtual machines with the same name exist, then provision_vm_folder is required parameter to identify uniqueness of the virtual machine. You can also set provision_vm_name_match to control how multiple matching VM names are handled.
          - The parameter is required if the virtual machine does not already exist.
          - This parameter is case sensitive.
        type: str
        required: true

      provision_vm_uuid:
        description:
          - The instance UUID of the virtual machine to manage.
          - This is required if provision_vm_name is not supplied.#
          - Note that a supplied UUID will be ignored on virtual machine creation, as VMware creates the UUID internally. If virtual machine does not exist, then this parameter is ignored.
        type: str
        required: false

      provision_vm_cluster:
        description:
          - The name of the cluster where the virtual machine will run.
        type: str
        required: false

      provision_vm_esxi_hostname:
        description:
          - The ESXi hostname where the virtual machine will run. This is a required parameter if provision_vm_cluster is not set.
          - provision_vm_esxi_hostname and provision_vm_cluster are mutually exclusive parameters.
          - This parameter is case sensitive.
        mutually_exclusive:
          - provision_vm_esxi_hostname
          - provision_vm_cluster
        type: str
        required: false

      provision_vm_datacenter:
        description:
          - The name of the datacenter where the virtual machine will run.
          - This parameter is case sensitive.
          - Default is "ha-datacenter"
        default: "ha-datacenter"
        type: str
        required: false

      provision_vm_folder:
        description:
          - Absolute path to the folder where the VM will exist.
          - The folder should include the datacenter. A single ESXi's datacenter is ha-datacenter.
          - This parameter is case sensitive.
          - If multiple machines are found with same name, this parameter is used to identify uniqueness of the virtual machine.
        type: str
        required: false

      provision_vm_datastore:
        description:
          - Specify datastore or datastore cluster to use for the virtual machine backend storage.
          - This parameter takes precedence over the provision_vm_disk.datastore parameter.
          - This parameter is case sensitive.
          - If multiple machines are found with same name, this parameter is used to identify uniqueness of the virtual machine.
        type: str
        required: false
...

EOF
```
