pulp-secret
===========

This role imports [Pulp](http://www.pulpproject.org/) keys from filesystem into
OpenShift. See the [OSBS
documentation](https://github.com/projectatomic/osbs-client/blob/master/docs/secret.md)
for more information.

This role is part of
[ansible-osbs](https://github.com/projectatomic/ansible-osbs/) playbook for
deploying OpenShift build service. Please refer to that github repository for
[documentation](https://github.com/projectatomic/ansible-osbs/blob/master/README.md)
and [issue tracker](https://github.com/projectatomic/ansible-osbs/issues).

Role Variables
--------------

You can import the keys either from the machine running ansible or from the
managed remote host. In the first case you have to set the
`pulp_secret_local_dir` variable to the directory containing the certificate
and the key. The files in the directory will first be copied to temporary
directory on the remote machine and then imported.

    pulp_secret_local_dir: /home/mmilata/.pulp

If the keys are already present on the remote machine, set
`pulp_secret_remote_dir` to the directory in question.

    pulp_secret_remote_dir: /root/.pulp

Please note that exactly one of these two variables has to be defined.

The name of the secret in OpenShift is defined by the `pulp_secret_name`
variable.

    pulp_secret_name: pulpsecret

The secret has to be associated with a service account. This service account
can be set by the `pulp_secret_service_account` variable.

    pulp_secret_service_account: builder

We need a kubeconfig file on the remote machine in order to talk to OpenShift.
Its location is contained in the `pulp_secret_kubeconfig`.

    pulp_secret_kubeconfig: /etc/openshift/master/admin.kubeconfig

Example Playbook
----------------

Following playbook imports the keys from my home directory on the machine where
ansible is executed. You may need to run something like this after the current
set of keys expires.

    - hosts: builders
      roles:
         - role: pulp-secret
           pulp_secret_local_dir: /home/mmilata/.pulp

Similar playbook from importing the keys directly from filesystem of the
managed machine:

    - hosts: builders
      roles:
         - role: pulp-secret
           pulp_secret_remote_dir: /mnt/sync/pulp_secrets

License
-------

BSD

Author Information
------------------

Martin Milata &lt;mmilata@redhat.com&gt;
