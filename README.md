# Ansible Gentoo
This vagrant box produces an error when attempting to check the status of a service with Ansible.
To replicate, start the vagrant box and then ```ssh``` into it.
```bash
vagrant up
vagrant ssh
```
Inside the vagrant box run
```bash
cd /vagrant
ansible-playbook playbook.yml -vvvv
```
Will produce the following error
```
No config file found; using defaults
 [WARNING]: Host file not found: /etc/ansible/hosts

 [WARNING]: provided hosts list is empty, only localhost is available

Loading callback plugin default of type stdout, v2.0 from /usr/lib64/python3.4/site-packages/ansible/plugins/callback/__init__.py

PLAYBOOK: playbook.yml *********************************************************
1 plays in playbook.yml

PLAY [localhost] ***************************************************************

TASK [setup] *******************************************************************
Using module file /usr/lib64/python3.4/site-packages/ansible/modules/core/system/setup.py
<127.0.0.1> ESTABLISH LOCAL CONNECTION FOR USER: vagrant
<127.0.0.1> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo ~/.ansible/tmp/ansible-tmp-1485728475.1546552-136258276406474 `" && echo ansible-tmp-1485728475.1546552-136258276406474="` echo ~/.ansible/tmp/ansible-tmp-1485728475.1546552-136258276406474 `" ) && sleep 0'
<127.0.0.1> PUT /tmp/tmpgb4ji_2c TO /home/vagrant/.ansible/tmp/ansible-tmp-1485728475.1546552-136258276406474/setup.py
<127.0.0.1> EXEC /bin/sh -c 'chmod u+x /home/vagrant/.ansible/tmp/ansible-tmp-1485728475.1546552-136258276406474/ /home/vagrant/.ansible/tmp/ansible-tmp-1485728475.1546552-136258276406474/setup.py && sleep 0'
<127.0.0.1> EXEC /bin/sh -c 'sudo -H -S -n -u root /bin/sh -c '"'"'echo BECOME-SUCCESS-lpcxxfjkwxbepqicrhaitlvwbgeeoftw; /usr/bin/python3.4 /home/vagrant/.ansible/tmp/ansible-tmp-1485728475.1546552-136258276406474/setup.py; rm -rf "/home/vagrant/.ansible/tmp/ansible-tmp-1485728475.1546552-136258276406474/" > /dev/null 2>&1'"'"' && sleep 0'
ok: [localhost]

TASK [service] *****************************************************************
task path: /vagrant/playbook.yml:5
Running service
Using module file /usr/lib64/python3.4/site-packages/ansible/modules/core/system/service.py
<127.0.0.1> ESTABLISH LOCAL CONNECTION FOR USER: vagrant
<127.0.0.1> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo ~/.ansible/tmp/ansible-tmp-1485728480.7279906-46765693117684 `" && echo ansible-tmp-1485728480.7279906-46765693117684="` echo ~/.ansible/tmp/ansible-tmp-1485728480.7279906-46765693117684 `" ) && sleep 0'
<127.0.0.1> PUT /tmp/tmphqtgchb0 TO /home/vagrant/.ansible/tmp/ansible-tmp-1485728480.7279906-46765693117684/service.py
<127.0.0.1> EXEC /bin/sh -c 'chmod u+x /home/vagrant/.ansible/tmp/ansible-tmp-1485728480.7279906-46765693117684/ /home/vagrant/.ansible/tmp/ansible-tmp-1485728480.7279906-46765693117684/service.py && sleep 0'
<127.0.0.1> EXEC /bin/sh -c 'sudo -H -S -n -u root /bin/sh -c '"'"'echo BECOME-SUCCESS-wmmnestsglioaloffnejbxcdunpmikze; /usr/bin/python3.4 /home/vagrant/.ansible/tmp/ansible-tmp-1485728480.7279906-46765693117684/service.py; rm -rf "/home/vagrant/.ansible/tmp/ansible-tmp-1485728480.7279906-46765693117684/" > /dev/null 2>&1'"'"' && sleep 0'
An exception occurred during task execution. The full traceback is:
Traceback (most recent call last):
  File "/tmp/ansible_ckjkjhx8/ansible_module_service.py", line 1552, in <module>
    main()
  File "/tmp/ansible_ckjkjhx8/ansible_module_service.py", line 1508, in main
    service.get_service_status()
  File "/tmp/ansible_ckjkjhx8/ansible_module_service.py", line 575, in get_service_status
    rc, status_stdout, status_stderr = self.service_control()
  File "/tmp/ansible_ckjkjhx8/ansible_module_service.py", line 899, in service_control
    rc_state, stdout, stderr = self.execute_command("%s %s %s" % (svc_cmd, self.action, arguments), daemonize=True)
  File "/tmp/ansible_ckjkjhx8/ansible_module_service.py", line 262, in execute_command
    return json.loads(data)
  File "/usr/lib64/python3.4/json/__init__.py", line 318, in loads
    return _default_decoder.decode(s)
  File "/usr/lib64/python3.4/json/decoder.py", line 343, in decode
    obj, end = self.raw_decode(s, idx=_w(s, 0).end())
  File "/usr/lib64/python3.4/json/decoder.py", line 361, in raw_decode
    raise ValueError(errmsg("Expecting value", s, err.value)) from None
ValueError: Expecting value: line 1 column 1 (char 0)

fatal: [localhost]: FAILED! => {
    "changed": false,
    "failed": true,
    "invocation": {
        "module_args": {
            "name": "net.eth0",
            "state": "started"
        },
        "module_name": "service"
    },
    "module_stderr": "Traceback (most recent call last):\n  File \"/tmp/ansible_ckjkjhx8/ansible_module_service.py\", line 1552, in <module>\n    main()\n  File \"/tmp/ansible_ckjkjhx8/ansible_module_service.py\", line 1508, in main\n    service.get_service_status()\n  File \"/tmp/ansible_ckjkjhx8/ansible_module_service.py\", line 575, in get_service_status\n    rc, status_stdout, status_stderr = self.service_control()\n  File \"/tmp/ansible_ckjkjhx8/ansible_module_service.py\", line 899, in service_control\n    rc_state, stdout, stderr = self.execute_command(\"%s %s %s\" % (svc_cmd, self.action, arguments), daemonize=True)\n  File \"/tmp/ansible_ckjkjhx8/ansible_module_service.py\", line 262, in execute_command\n    return json.loads(data)\n  File \"/usr/lib64/python3.4/json/__init__.py\", line 318, in loads\n    return _default_decoder.decode(s)\n  File \"/usr/lib64/python3.4/json/decoder.py\", line 343, in decode\n    obj, end = self.raw_decode(s, idx=_w(s, 0).end())\n  File \"/usr/lib64/python3.4/json/decoder.py\", line 361, in raw_decode\n    raise ValueError(errmsg(\"Expecting value\", s, err.value)) from None\nValueError: Expecting value: line 1 column 1 (char 0)\n",
    "module_stdout": "",
    "msg": "MODULE FAILURE"
}
        to retry, use: --limit @/vagrant/playbook.retry

PLAY RECAP *********************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=1  
```