# kubevirt-crc-windows-tutorial
Running a Window Framework (NOT .NET Core) app on Kubernetes using CodeReady Containers and Kubevirt

This tutorial will guide you through the process of getting kubevirt running inside of OpenShift, and then using kubevirt to host a Windows VM in OpenShift. That Windows VM will be running an IIS-powered web site and a .NET Framework WCF service application.

## Glossary/Acronyms
CLI: Command-Line Interface  
CRC: CodeReady Containers  
VM: Virtual Machine  

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
Now, add 70GB to the VM by running the makebig script:  
`./makebig.sh`



### Start
Now we can start CRC and proceed with the tutorial.  
`crc start`

## Install kubevirt Operator  
This first part will get the current version number (e.g. 0.25.0) into an environment variable.  
export KUBEVIRT_VERSION=$(curl -s https://api.github.com/repos/kubevirt/kubevirt/releases/latest | jq -r .tag_name)  
echo $KUBEVIRT_VERSION  

kubectl create -f https://github.com/kubevirt/kubevirt/releases/download/${KUBEVIRT_VERSION}/kubevirt-operator.yaml

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