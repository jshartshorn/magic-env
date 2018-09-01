General Notes
-------------

  - These roles still need integrated into the main Stable Guard ansible scripts. I am uncomfortable modifying this source due to the lack of an environment to test in/with. We should really look at getting a dev/test/staging environment up...or better yet... ephemeral environments (DevOps).
  - Assumes host infra is up and accessible from ansible control point and user.
  - Assumes Zabbix 3.4. Change the zabbix repo in the group_vars folder when appropriate.
  - Assumes ansible 2.x or later. Unit tested with 2.6.
  - server, agent and proxy configs are in the templates folder.
  - Ansible version should be > 2.3.
  - My local install uses a docker image based on trusty due to ssh changes from trusty -> xenial.
  - I avoided using ansible galaxy but there is a possible option of use -> Werner Dijkerman's galaxy roles for zabbix -> https://galaxy.ansible.com/dj-wasabi


TODO
----

  - This needs tested with the full Stable Gaurd stack and infra. Currently, there is no dev, test, stage to enable easy testing. Therefore, these scripts have only been tested on a local machine using docker.
  - The zabbix version is hard coded in a few places for example in the repo vars and sql script vars. It would be ideal to have this more parameterized and DRY.
  - We should upgrade to Ansible 2.5 or later. Current dev version is 2.6. 2.5 has better support for zabbix.
  - zabbix agent task needs to have a longer timeout with more hosts. Currently, 10 seconds may timeout.


Setup/Configure Tasks
-----

  1. Change ansible.cfg to your settings/liking.
  1. Change `hosts` file according to your needs. I used docker.
  1. Change values specified in group_vars/* files.


Zabbix Agents
------

  1. The zabbix agent will be deployed to all hosts in the zabbix_agents host group. This value can be manually or dynamically updated.


Running playbooks
-----------------

		ansible-playbook -i <hosts_file> <playbook>

Example(s):

		ansible-playbook -i hosts zabbix_server.yml
    ansible-playbook -i hosts zabbix_agent.yml
    ansible-playbook -i hosts zabbix_proxy.yml
