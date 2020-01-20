# kubevirt-crc-windows-tutorial
Running a Window Framework (NOT .NET Core) app on Kubernetes using CodeReady Containers and Kubevirt

This tutorial will guide you through the process of getting kubevirt running inside of OpenShift, and then using kubevirt to host a Windows VM in OpenShift. That Windows VM will be running an IIS-powered web site and a .NET Framework WCF service application.

## Glossary
VM: Virtual Machine  
CRC: CodeReady Containers  
CLI: Command-Line Interface  

## Prerequisites
CodeReady Containers  
`kubectl` CLI  
`oc` CLI  
`virtctl` CLI  
`cdi` CLI  

## Prepare CRC
The default VM that is created by CRC is too small at 30GB. It must be resized to just over 100GB in order for this tutorial to work.

The steps are:
1. Create a VM
2. Stop CRC
3. Resize the VM
4. Start CRC and continue with the tutorial.

### Set VM memory
Make sure the VM has enough RAM in order to keep performance acceptable. More is better in this case. We'll set aside about 12GB of RAM.

`crc config set memory 12000`


### Start in order to be a VM
`crc start`

### Stop
After CRC has started, there is no reason (yet) to sign in. Immediately stop CRC (and the VM in the procss) so the VM can be resized.

`crc stop`

### Resize
Now, add 70GB to the VM:
`export CRC_MACHINE_IMAGE=${HOME}/.crc/machines/crc/crc`  

`qemu-img resize ${CRC_MACHINE_IMAGE} +70G`  

`cp ${CRC_MACHINE_IMAGE} ${CRC_MACHINE_IMAGE}.ORIGINAL`  

`virt-resize --expand /dev/sda3 ${CRC_MACHINE_IMAGE}.ORIGINAL ${CRC_MACHINE_IMAGE}`  

`rm ${CRC_MACHINE_IMAGE}.ORIGINAL`  



### Start
Now we can start CRC and proceed with the tutorial.

## Install kubevirt

## Install CDI

## Tweak file permissions

## Upload VM images

## Create VM

## Create Service

## Create Routes

## View web site

## Use web service

## Install .NET Core service as replacement

## Switch route to .NET Core service