+++
title = "Set_crontab"
date = 2018-12-17T16:04:36+05:30
tags = [""]
categories = [""]
draft = false
+++


How to create a cronjob using Ansible:

```yaml
---

- name: Playbook to add new entries in crontab
  hosts: all
  remote_user: user_name
  tasks:
     - name: check whether user_name has permission to create crontab
       shell: 'grep "user_name" /etc/cron.allow'
       register: user_status
       failed_when: "user_status.rc == 2"
       changed_when: false
       become: yes

     - name: Add user to /etc/cron.allow if it doesn't exist
       shell: 'echo "user_name" | sudo tee -a /etc/cron.allow'
       when:  user_status.rc == 1

     - name: add new crontab entry if the user is newly added
       shell: 'echo "43 15 * * * /bin/bash /home/user_name/script_name.sh > /dev/null 2>&1" | crontab -'
       when:  user_status.rc == 1
       register: new_entry

     - name: add new crontab entry along with old entries
       shell: '(crontab -l ; echo "43 15 * * * /bin/bash home/user_name/script_name.sh > /dev/null 2>&1") | crontab -'
       when: new_entry is skipped

     - name: Check whether crontab entry is added or not
       command: crontab -l
       changed_when: false

     - name : restart the crond service
       service:
          name: crond
          state: restarted
       become: yes
```

Tested on CentOS6.10 with ansible version 2.6.7.

