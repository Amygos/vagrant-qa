# Vagrant QA environment

## QA Process Steps

1. Merge all pull requst
1. Wait for packages to be upload in testing
1. Prepare QA environment
1. Write tests Cases and assing to relative test env
1. Add "testing" tag to the issue

## Prepare QA environment

* Create Vagrantfile, playbook.yml and requirements.yml, you can find exemples in the `examples_qa_envs/` directory.
* Install and configure `gist` https://github.com/defunkt/gist
* Create a new gist with the QA environment, .eg:
```
gist  -d "Amygos/dev#1 QA ENV 1" Vagrantfile playbook.yml requirements.ym
```
* Copy the relative gist link or use `-c` options for copy the resulting link to the clipboard
* Add the link to the QA test cases in the relative issue.

## Execute QA test

1. Download/clone the QA environment from the gist
1. `vagrant up`
1. Follow the QA steps
1. Report the QA result

In case of multiple QA test case with the same QA environment, make sure to clean the environment with:
`vagant destroy` before `vagant up`

## QA environments examples

* [**qa env 1**](examples_qa_envs/qa_env_1/): simple QA environment with one interface red (host nat) and one interface green (local private network)
* [**qa env 2**](examples_qa_envs/qa_env_2/): simple QA environment with one interface red (host nat) and one interface green (bridge to host interface)
* [**qa env webtop5**](examples_qa_envs/qa_env_webtop5/): QA environment with Webtop5 installed and local ldap as Accounts provider
* [**qa env enterprise**](examples_qa_envs/qa_env_enterprise): QA environment with Nethesis enterprise repository installed
* **qa env nethvoice**: QA environment with Nethesis enterprise repository installed

## Ansible role list
List of common ansible roles used for create QA environments:

* [amygos.nethserver_vagrant_base_setup](https://galaxy.ansible.com/Amygos/nethserver_vagrant_base_setup): role used for first config setup, will be the first role to use in most of the cases
* [amygos.nethserver_install_packages](https://galaxy.ansible.com/Amygos/nethserver_install_packages): role for install lists of list of packages
* [amygos.nethserver_accounts_provider](https://galaxy.ansible.com/Amygos/nethserver_accounts_provider): role for install Accounts provider
* [amygos.nethesis_addrepos](https://galaxy.ansible.com/Amygos/nethesis_addrepos): role for install Nethesis enterprise repository.

## Libvirt Vagrant provider

For disable password prompt: https://lalatendu.org/2016/02/24/get-rid-of-password-prompt-for-vagrant-commands-on-libvirt/
```
# cd  /etc/polkit-1/localauthority/50-local.d
# cat vagrant.pkla 
[Allow lmohanty libvirt management permissions]
Identity=unix-user:<USER_NAME>
Action=org.libvirt.unix.manage
ResultAny=yes
ResultInactive=yes
ResultActive=yes
```
Change `<USER_NAME>` with your username
