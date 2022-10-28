README
======

This is an ansible role designed to automate the conversion of CentOS to RHEL

This is NOT production ready. You will find bugs / errors.

This has been minimally tested to convert from a fresh install of CentOS 8 to RHEL 8 using Red Hat Satellite as a content source.

The suggestion is that you clone / fork and use this as a basis or template.

How to use
----------

If using Ansible Tower create a new project and use this repo as a content source. 

If using Ansible Engine this is not available on ansible-galaxy. Use git clone and set the directory it is downloaded to as a role source in your ansible.cfg file.

Variables to define
-------------------

conversion_method - acceptable values are "satellite" or "RHN". This deines the content source and where the system is subscribed to.

---

Variables required if using Satellite to convert:

satellite_fqdn - the fqdn of your satellite server. This is the server the machine will be registered to.

activation_key - This is the activiation key used by your satellite server

organisation - This is the organisation used by your satellilte server

---

Variables Required if converting via RHN:

rhsm_username - Red hat username. Recommended practice to keep this in an ansible vault or satellite credential

rhsm_password - Password for red hat. Recommended practice to keep this in an ansible vault or satellite credential

rhsm_pool - pool ID of the subscription used.

---

Other Variables

reboot_bool - Default is False. If false a full conversion will not be completed. Full conversion requires up to 2 reboots. If false this will only install the convert2rhel tool and the certs/keys required to do so. If True a full conversion will be attempted

upgrade_bool - Default is False. Determines if yum update is executed before upgrade

repoconfig_bool - Default is False. Determines if the default Yum Repo's are edited. WARNING if set to true this uses the shell module to execute and is not idempotent. Setting to True may have unintended consequences. If performing an updgrade via upgrade_bool this will be required to be set to True. 

kernel_package - an up to date kernel is required to perform a conversion. Define the package name using this variable. Default value works with CentOS 8.5


