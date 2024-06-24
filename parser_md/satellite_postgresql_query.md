Satellite PostgreSQL database queries
=====================================

This module contains the following parsers:

SatelliteAdminSettings - command ``psql -d foreman -c 'select name, value, "default" from settings where name in ('destroy_vm_on_host_delete', 'unregister_delete_host') --csv'``
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
SatelliteComputeResources - command ``psql -d foreman -c 'select name, type from compute_resources' --csv``
-----------------------------------------------------------------------------------------------------------
SatelliteCoreTaskReservedResourceCount - command ``psql -d pulpcore -c 'select count(*) from core_taskreservedresource' --csv``
-------------------------------------------------------------------------------------------------------------------------------
SatelliteIgnoreSourceRpmsRepos - command ``psql -d foreman -c "select id, name from katello_root_repositories where ignorable_content like '%srpm%' and mirroring_policy='mirror_complete'" --csv``
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
SatelliteKatellloReposWithMultipleRef - command ``psql -d foreman -c "select repository_href, count(*) from katello_repository_references group by repository_href having count(*) > 1;" --csv``
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
SatelliteLogsTableSize - command ``psql -d foreman -c "select pg_total_relation_size('logs') as logs_size" --csv``
------------------------------------------------------------------------------------------------------------------
SatelliteProvisionParamSettings - command ``psql -d foreman -c "select name, value from parameters where name='package_upgrade' and reference_id in (select id from operatingsystems where name='RedHat' and major='9')" --csv``
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
SatelliteQualifiedCapsules - command ``psql -d foreman -c "select name from smart_proxies where download_policy = 'background'" --csv``
---------------------------------------------------------------------------------------------------------------------------------------
SatelliteQualifiedKatelloRepos - command ``psql -d foreman -c "select id, name, url, download_policy from katello_root_repositories where download_policy = 'background' or url is NULL" --csv``
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
SatelliteRevokedCertCount - command ``psql -d candlepin -c "select count(cp_certificate.id) from cp_cert_serial inner join cp_certificate on cp_certificate.serial_id = cp_cert_serial.id where cp_cert_serial.revoked = 't'" --csv``
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
SatelliteRHVHostsCount - command ``psql -d foreman -c "select count(*) from hosts where "compute_resource_id" in (select id from compute_resources where type='Foreman::Model::Ovirt')" --csv``
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
SatelliteSCAStatus - command ``psql -d candlepin -c "select displayname, content_access_mode from cp_owner" --csv``
-------------------------------------------------------------------------------------------------------------------