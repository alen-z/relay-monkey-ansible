> This repository is part of Relay Monkey project.

## About
This Ansible playbook is used to run Relay Monkey Agent on instances provisioned by Terraform, created as part of Relay Monkey project.

## Usage
**Important:** Make sure you have inventory of instances created from Terraform output using Jinja. Terraform and Jinja repositories are available as part of Relay Monkey project. Docker container of our Relay Monkey Agent application is hosted in DigitalOcean container registry. This is why `DO_TOKEN` is used.
```shell
export DO_TOKEN=<digitalocean_token>
ansible-playbook -i ../relay-monkey-jinja/ansible_inventory.yml run_relay_monkey.yml
```

## Performance tweaks
```shell
export ANSIBLE_HOST_KEY_CHECKING=False
export ANSIBLE_PIPELINING=True
export ANSIBLE_SSH_EXTRA_ARGS="-o ControlMaster=auto -o ControlPersist=60s"
export ANSIBLE_FORKS=30
export ANSIBLE_CALLBACK_WHITELIST=profile_tasks
export ANSIBLE_STDOUT_CALLBACK=counter_enabled
```

## References
Create inventory YAML — https://docs.ansible.com/ansible/latest/plugins/inventory/yaml.html
Install Docker demo — https://github.com/do-community/ansible-playbooks/blob/master/docker_ubuntu1804/playbook.yml
Set Python 3 as default interpreter — https://linuxconfig.org/how-to-change-default-python-version-on-debian-9-stretch-linux
Ansible configuration variables — https://docs.ansible.com/ansible/latest/reference_appendices/config.html#default-stdout-callback
