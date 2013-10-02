Run the playbook:
----------------

`vagrant up`

Notes
-----

* Based almost 100% on: https://github.com/vikhyat/discourse-ansible
* Some small changes to work on Ansible 1.3
* Assumed to be running inside a Vagrant VM with host defined as in the `vagrant` inventory file.
* Uses monit instead of bluepill.

TODO
----

* Automate Postgres backups.
* Firewall with IPTables.
