1) Создать /etc/ansible/hosts и промежуточные директории c содержимым
```
---
prod-nodes:
  hosts:
    node01:
      ansible_host: HOST1_IP
    node02:
      ansible_host: HOST2_IP
    node03:
      ansible_host: HOST3_IP
  vars:
    ansible_user: SSH_USER_USERNAME
```
2) Создать ansible/tasks/setup_base_server.yml и промежуточные директории c содержимым
```
---
- name: setup base config
  become: yes
  hosts: "{{ host_to_setup }}"
  roles:
    - base_server
```
3) Из директории /etc/ansible запустить
```
ansible-playbook -i hosts -K -v tasks/setup_base_server.yml -e "host_to_setup=HOSTS_TO_SETUP" --tags=sshd
```
