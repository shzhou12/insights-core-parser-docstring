Satellite MongoDB Commands
==========================

Parsers included in this module are:

MongoDBStorageEngine - command ``mongo pulp_database --eval 'db.serverStatus().storageEngine'``
-----------------------------------------------------------------------------------------------
MongoDBNonYumTypeRepos - command ``mongo pulp_database --eval 'db.repo_importers.find({"importer_type_id": { $ne: "yum_importer"}}).count()'``
----------------------------------------------------------------------------------------------------------------------------------------------