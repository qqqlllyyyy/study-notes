## Database

Account information to connect to the database:

* Host: mlm.devdocker.marketo.com
* Account: root
* Password: marketo17

There is a `betamkto` database for each group (pod), and a `{{username}}Betacust` database for each instance (subscription).

* `betamkto.user`: Account & password information for the system. Note that the field `password_salt_updated_at_utc` is required to encrypt/decrypt the password.
* `betamkto.contact_info`: Account details for the system. (first name, last name, address, ...)
* `testBetacust.access_role`: Role information. For example, ID for `Abm User` is needed if we want to have access to ABM.
* `testBetacust.user_access_role`: Define role for each user. We need to have a record with userid `test@marketo.com` and access_role_id `26` (ID for `Abm User` in `access_role`).
* `testBetacust.access_capability`: Detailed permissions, for example, `Edit Named Account`.
* `testBetacust.access_grant`: Permissions for each role. Joint table for `access_role` and `access_capability`.


All named accounts are saved in table `mkt_account`.

All named account lists are saved in table `mkt_account_list`.
