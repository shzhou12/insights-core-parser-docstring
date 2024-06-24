OpenShift Get commands with configuration file
==============================================

The commands set is similar to the ``oc get`` commands. It is used to display openshift resources.
It uses the master configuration file rather than the default configuration when communicated with the client API.
It makes sure this command will only be executed on the master node of an OpenShift cluster.
This command will also not include the commands which display large size outputs.

Parsers included in this module are:

OcGetClusterRoleWithConfig - command ``oc get clusterrole --config /etc/origin/master/admin.kubeconfig``
--------------------------------------------------------------------------------------------------------

OcGetClusterRoleBindingWithConfig - command ``oc get clusterrolebinding --config /etc/origin/master/admin.kubeconfig``
----------------------------------------------------------------------------------------------------------------------