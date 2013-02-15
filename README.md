## BStack

A set of shell scripts to deploy an arbitrary number of instances on a node for various load testing purposes.


### Setup

These scripts need the usual suspects in Linux virtualization installed. Installing libvirt and qemu-kvm should get you there.

To configure edit `conf/settings` to suit your needs. Copy your template to the `VOLUMEPATH` indicated in the settings file to the indicated `TEMPLATE_NAME`. Make sure the template includes the node's ~root/.ssh/id_rsa.pub key in the `TEMPLATE_USER`'s ~/.ssh/authorized_keys. Finally:

    # source vars


### Usage

To deploy 25 instances, first setup the node networking and then create the VMs.

    # node_setup_networking
    # node_create_vms 25

To cleanup, simply delete the instances and teardown the networking setup.

    # node_delete_vms
    # node_teardown_networking

After creating the VMs, you can check how many are up and running with an IP allocated:

    # node_check_vms_running
    Numer of VMs up and running: 5

    test-vm-27299-1
    test-vm-27299-2
    test-vm-27299-3
    test-vm-27299-4
    test-vm-27299-5

Once the instances are up you can execute commands in parallel on each instance:

    # vms_execute_cmd "echo Hello..." 
    Hello...
    Hello...
    Hello...
    ...

Upload and download files:

    # vms_upload_file file
    file                                     100%    4     0.0KB/s   00:00    
    file                                     100%    4     0.0KB/s   00:00    
    file                                     100%    4     0.0KB/s   00:00    
    ...

    # vms_download_file file
    file                                     100%    4     0.0KB/s   00:00    
    file                                     100%    4     0.0KB/s   00:00    
    file                                     100%    4     0.0KB/s   00:00    
    ...
    Files downloaded to /root/bstack/downloaded

And ssh to a random sample:

    # vms_ssh_random

These should suffice to upload and run your scripts and download reports.


### Notes

For customizing instance definitions see `lib/domain.xml`.


### License

Simplified BSD. See the LICENSE file for details.
