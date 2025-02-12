Ansible role for Satellite 6 install
===========================

Role to install and do basic configuration of Red Hat Satellite 6.x on Red Hat Enterprise Linux (RHEL) 7.x


Requirements
------------

You will need Ansible installed for the workstation from where you are running the playbook and all the required subscriptions for Red Hat Enterprise Linux (RHEL) 7 and Red Hat Satellite 6 (or Red Hat Smart Management).

* Disk partitioning and storage requirements according to the official Satellite documentation:
  * [Satellite 6.5 - Storage Requirements and Guidelines](https://access.redhat.com/documentation/en-us/red_hat_satellite/6.5/html/installing_satellite_server_from_a_connected_network/preparing_your_environment_for_installation#hardware_storage_prerequisites)
  * [Satellite 6.4 - Storage Requirements and Guidelines](https://access.redhat.com/documentation/en-us/red_hat_satellite/6.4/html/installing_satellite_server_from_a_connected_network/preparing_your_environment_for_installation#hardware_storage_prerequisites)
  * [Satellite 6.3 - Storage Requirements and Recommendations](https://access.redhat.com/documentation/en-us/red_hat_satellite/6.3/html/installation_guide/preparing_your_environment_for_installation#hardware_storage_prerequisites)
  * [Satellite 6.2 - Storage Requirements and Recommendations](https://access.redhat.com/documentation/en-us/red_hat_satellite/6.2/html/installation_guide/preparing_your_environment_for_installation#hardware_storage_prerequisites)
* DNS
* NTP
* `satellite_deployment_manifest_path` variable defined 
* Satellite Manifest file hosted in the Ansible Bastion or available via HTTP or FTP

Role Variables
--------------

All variables are located in [``defaults/main.yml``](defaults/main.yml).


Dependencies
------------

There are no dependencies for this role.

Inventory File
----------

The inventory file example for this role is in [``playbook_example/hosts.target``](playbook_example/hosts.target).

How to run the playbook
------------------------

1. To run the playbook first you need to create and download the manifest:
   * Go to the [Subscriptions Allocations](https://access.redhat.com/management/subscription_allocations) section in the Red Hat Customer Portal.
   * Click the "Create New Subscription Allocation" button or the "New Subscription Allocation" if you already have other allocations.
   * Name field: Enter the name for this allocation (using a reference to the Satellite host for later identification is recommended, for ex. organization-satellite-01).
   * Type field: Select the Satellite version (this playbook currently supports versions of Satellite 6.1 to 6.5)
   * Click the "Create" button.
2. Now we are going to attach a subscription.
   * Click the "Subscriptions" tab for the created allocation
   * Click the "Add Subscriptions" button.
   * Select the subscriptions you want to add to this Satellite's manifest.
   * Click the "Submit" button   
3. After attaching the subscriptions to the allocation we have to download the manifest file:
   * Click "Download manifest"
4. Copy the downloaded file inside the `/files` directory on the role and name it `satellite_manifest.zip`
5. Finally update the variable file in `defaults/main.yml` in your playbook and set all mandatory variables for the role.

You can see an [example of the playbook config here](./playbook_example/config.yml)

```
cd playbook_example
ansible-playbook -i hosts.target -e '{satellite_deployment_vars: ./vars/main.yml}' config.yml
```

Run the playbook, see [README of example playbook](./playbook_example/README.md).

Notes
-----------

This role will take some time to run depending on the number of repositories set to sync.


License
-------

MIT

Author Information
------------------

Julio Villarreal Pelegrino <julio@linux.com> more at: http://wwww.juliovillarreal.com

**Contributors:**

* Petr Balogh - <petr.balogh@gmail.com>
* Joe Pisciotta - <josephpisciott@mac.com>
* Nick Poyant - <npoyant@redhat.com>
* Cameron Wyatt - cwyatt@redhat.com
* Christian Stankowic - <info@cstan.io>
* Leonardo Gallego - leogallego[@]redhat.com
