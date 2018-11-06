# QA Process

## Steps

1. Merge all pull requst
1. Wait for packages to be upload in testing
1. Prepare QA envirioments
1. Write tests Cases and assing to relative test env
1. Add "testing" tag to the issue

## Prepare QA envirioments

* Create Vagrantfile and ansible playbook as in the example directory `test_issue`
* install and configure gist https://github.com/defunkt/gist
* Create a new gist with the QA envirioment, ex:

```console
gist  -sd "Amygos/dev#1 QA ENV 1" Vagrantfile playbook.yml requirements.yml"
```
* Copy the relative gist link or user `-c` options for copy the resulting link to the clipboard
* Add the link to the QA test cases

## Execute QA test

1. Download/clone the QA enviroment
1. `vagrant up`
1. follow the QA steps
1. report the QA result

In case of multiple QA test case with the same QA enviroment, make sure to clean the enviroment with:
`vagant destroy` before `vagant up`
