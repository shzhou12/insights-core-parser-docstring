OpenShift Get commands
======================

``oc get`` command is from openshift used to list the usage info - e.g.
pods info, dc info, services info, etc.  This shared parser is used to parse
``oc get XX --all-namespaces -o yaml`` command information. Parameters
"--all-namespaces" means collecting information from all projects and "-o yaml"
means the output is in YAML format.

Parsers included in this module are:

OcGetBc - command ``oc get bc -o yaml --all-namespaces``
--------------------------------------------------------

OcGetBuild - command ``oc get build -o yaml --all-namespaces``
--------------------------------------------------------------

OcGetDc - command ``oc get dc -o yaml --all-namespaces``
--------------------------------------------------------

OcGetEgressNetworkPolicy - command ``oc get egressnetworkpolicy -o yaml --all-namespaces``
------------------------------------------------------------------------------------------

OcGetEndPoints - command ``oc get endpoints -o yaml --all-namespaces``
----------------------------------------------------------------------

OcGetEvent - command ``oc get event -o yaml --all-namespaces``
--------------------------------------------------------------

OcGetNode - command ``oc get nodes -o yaml``
--------------------------------------------

OcGetPod - command ``oc get pod -o yaml --all-namespaces``
----------------------------------------------------------

OcGetProject - command ``oc get project -o yaml --all-namespaces``
------------------------------------------------------------------

OcGetPv - command ``oc get pv -o yaml --all-namespaces``
--------------------------------------------------------

OcGetPvc - command ``oc get pvc -o yaml --all-namespaces``
----------------------------------------------------------

OcGetRc - command ``oc get rc -o yaml --all-namespaces``
--------------------------------------------------------

OcGetRole - command ``oc get role -o yaml --all-namespaces``
------------------------------------------------------------

OcGetRolebinding - command ``oc get rolebinding -o yaml --all-namespaces``
--------------------------------------------------------------------------

OcGetRoute - command ``oc get route -o yaml --all-namespaces``
--------------------------------------------------------------

OcGetService - command ``oc get service -o yaml --all-namespaces``
------------------------------------------------------------------

OcGetConfigmap - command ``oc get configmap -o yaml --all-namespaces``
----------------------------------------------------------------------

Examples:
    >>> type(setting_dic)
    <class 'insights.parsers.openshift_get.OcGetService'>
    >>> setting_dic.data['items'][0]['kind']
    'Service'
    >>> setting_dic.data['items'][0]['spec']['clusterIP']
    '172.30.0.1'
    >>> setting_dic.data['items'][0]['metadata']['name']
    'kubernetes'
    >>> setting_dic.data['items'][1]['metadata']['name']
    'router-1'
    >>> "zjj" in setting_dic.data['items'][1]['metadata']['namespace']
    True