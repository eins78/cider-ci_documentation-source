---
title: Install
---
{::options parse_block_html="true" /}

# Installing Cider-CI 
{:.no_toc}
Cider-CI is open source and can be installed with little effort. This page
guides through the process of installing a Cider-CI environment.


### Table of Contents 
{:.no_toc}
* Will be replaced with the ToC, excluding the "Contents" header
{:toc}



## Environment Prerequisites 

<div class="row"> <div class="col-md-6">

Ansible must be present on the *control* machine. See the [Install][] page of
the Ansible Documentation. We use a fairly recent version (≥ 1.9 at the time of
writing) of Ansible. The operating system on the controller is not relevant. We
use Mac OS X and various Linux variants. 

The Ansible setup supports Ubuntu 14.04 or Debian 8. The working account on the
**control machine**  must have **ssh access to the server and executors**.
A setup with SSH keys and without passwords is the most straight forward
configuration. 

The server and executors must reach each other via the **https** protocol (port
443) to function properly. The **example setup** assumes that all machines have
**fixed ipv4 addresses**. **Custom configuration** of protocol and port, as
well as names instead of addresses is **possible** but outside the scope of
this documentation.

</div> <div class="col-md-6">

[![Environment](/installation/environment.svg)](/installation/environment.svg)


</div> </div>


## Step by Step Install Procedure for a Demo Environment

The following example uses one machine in the role of the server and executor.


1.  We check out the [Cider-CI main project][] including all sub-projects inside 
    the control machine: 

    `git clone --recursive https://github.com/cider-ci/cider-ci.git` 

2. We descend into the ansible-setup directory.

    `cd cider-ci/ansible-setup` 

3. We adjust the host ip within the `hosts_demo_single` file: 


      [demo]
      demo-machine ansible_ssh_host=192.168.0.31 ansible_ssh_user=root


4. We invoke ansible-playbook to trigger the install: 

    `ansible-playbook -i hosts_example play_site.yml -e 'system_admin_password=secret system_admin_login=admin'`


## Adding Traits 

The demo installation will provide the traits `linux` and `bash` for each
executor. They suffice to run the jobs of the [Bash Demo Project for
Cider-CI][]. 

### Adding Traits provided by the Ansible Setup 

A set of additional traits can be automatically installed with

`ansible-playbook -i hosts_example play_traits.yml`

### Adding Custom Traits

A custom trait can be added by adding a corresponding line to the file
`/etc/cider-ci/traits.txt`. 


## Production Environment 

The server for a production environment should have at least 4GB of memory.
A fast disk is also recommended. Requirements for the executors depend on the
use case. 

The procedure for installing a production environment is exactly the same as
for the demo environment. However, the parameters for the example environment
are far from optimal. The [Cider-CI Ansible Setup] contains the hosts file
`hosts_zhkd_ci3` which is more appropriate to be used as a template in this
case. The directories `host_vars` and `group_vars` contain further files to be
used as templates and to be customized. 



  [Bash Demo Project for Cider-CI]: https://github.com/cider-ci/cider-ci_demo-project-bash
  [Cider-CI Ansible Setup]: https://github.com/cider-ci/cider-ci_ansible-setup
  [Cider-CI main project]: https://github.com/cider-ci/cider-ci
  [Install]: http://docs.ansible.com/intro_installation.html
