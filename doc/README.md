## OpenCrowbar Hardware Workloads

If you are using OpenCrowbar with the Hardware workload, then please review this documentation.

### Attach to BMC Network

By default, Crowbar sets up the BMC network from 192.168.128.21/22 and up.  That network will be bridged between your docker admin and your external NIC.  

If you'd like to connect to that network on your local system then you need to bind an IP for your desktop to that network:  `sudo ip a add 192.168.128.2/22 dev docker0`

### RAID Tools

Before Crowbar can configure RAID, you must download the correct utilities.  Crowbar does NOT perform this download due to licensing considerations of the tools.

You need to perform this step if you see the following error:

`STDOUT: SAS2IRCU_P19.zip not present at http://192.168.124.10:8091/files/raid`

*Note* The directory which you should place the file is different depending on weather crowbar is running in a Docker container or if it is running on a native OS

Steps on a native OS (Not in a Docker container):
  1. visit the following LSI pages in a _WEB BROWSER_ and accept the EULA
    1. [[http://www.lsi.com/downloads/Public/Host%20Bus%20Adapters/Host%20Bus%20Adapters%20Common%20Files/SAS_SATA_6G_P19/SAS2IRCU_P19.zip]]
    1. [[http://www.lsi.com/downloads/Public/RAID%20Controllers/RAID%20Controllers%20Common%20Files/8.07.14_MegaCLI.zip]]
    1. [[http://www.lsi.com/downloads/Public/Host%20Bus%20Adapters/Host%20Bus%20Adapters%20Common%20Files/SAS_SATA_12G_P8/SAS3IRCU_P8.zip]]
  1. copy the three downloaded files copied into: `/tftpboot/files/raid`
  1. update the permissions to allow guest reading: `chmod 664 *`

Steps with Docker:
  1. mkdir ~/.cache/opencrowbar/tftpboot/files/raid 
  1. cd ~/.cache/opencrowbar/tftpboot/files/raid
  1. visit the following LSI pages in a _WEB BROWSER_ and accept the EULA
    1. [[http://www.lsi.com/downloads/Public/Host%20Bus%20Adapters/Host%20Bus%20Adapters%20Common%20Files/SAS_SATA_6G_P19/SAS2IRCU_P19.zip]]
    1. [[http://www.lsi.com/downloads/Public/RAID%20Controllers/RAID%20Controllers%20Common%20Files/8.07.14_MegaCLI.zip]]
    1. [[http://www.lsi.com/downloads/Public/Host%20Bus%20Adapters/Host%20Bus%20Adapters%20Common%20Files/SAS_SATA_12G_P8/SAS3IRCU_P8.zip]]
  1. copy the three downloaded files copied into: `~/.cache/opencrowbar/tftpboot/files/raid`
  1. update the permissions to allow guest reading: `chmod 664 *`

*IMPORTANT* You should check [[raid/chef/roles/raid-tools-install/role-template.json]] to confirm that the file names are correct.

> You need to do these steps for even if the hardware (e.g.: KVM) does not need the libraries. 
  

