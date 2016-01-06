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

The role imports the keys from the machine running ansible. You have to set the
`pulp_secret_local_dir` variable to the directory containing the certificate
and the key.

    pulp_secret_local_dir: /home/mmilata/.pulp

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

License
-------

BSD

Author Information
------------------

Martin Milata &lt;mmilata@redhat.com&gt;
