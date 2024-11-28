# Ansible && Molecule on docker dev env

## 1.install pipx

```zsh
brew install pipx
pipx ensurepath
sudo pipx ensurepath --global # optional to allow pipx actions with --global argument
```

## 2.istall molecule

```zsh
pipx install --include-deps ansible

pipx inject --include-apps ansible ansible-lint

pipx inject --include-apps ansible molecule

pipx inject ansible 'molecule-plugins[docker]'

pipx install yamllint
```

## 3.create a collections folder and add your roles collections

```zsh
# the collection folder is a workspase to stor collections
# you can have multiples collections  
ansible-galaxy collection init [collection_folder].[collection]
```

## 4.create a role on the collectiom

```zsh
cd [collection_folder]/[collection]/roles/  
ansible-galaxy role init my_role
```

## 5.add tasks etc ... to your role

```zsh
vim my_role/tasks/main.yml
```

main.yml

```yaml
---
- name: Task is running from within the role
  ansible.builtin.debug:
    msg: "This is a task from my_role."
```

## 5.on [collection_folder] cretate a dir called *playbooks*

```zsh
mkdir [collection]/playbooks
```

## 6.on the playbooks dir create the playbook to call the role

```zsh
vim [collection_folder]/playbooks/my_playbook.yml
```

my_playbook.yaml

```yaml
---
- name: Test new role from within this playbook
  hosts: localhost
  gather_facts: false
  tasks:
    - name: Testing role
      ansible.builtin.include_role:
        name: mycollections.infrastructure.my_role
        tasks_from: main.yml
```

## 7.create a *extentions* folder on your collection

```zsh
mkdir [collection]/extentions
```

## 8.initiate molecule senario

```zsh
cd [collection]/extentions
molecule init scenario
ls molecule/default 
    converge.yml        create.yml        destroy.yml        molecule.yml 
```

## 8.change the container base to be used

change molecule [collection]/extentions/molecule/default/*converge.yaml*

```yaml
---
driver:
  name: docker
platforms:
  - name: instance
    image: [name]:[tag]
    privileged: true
    pre_build_image: true
```
