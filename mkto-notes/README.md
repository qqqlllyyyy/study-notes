
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

## Test Files

Since abm service is not setup locally, we can use the test file to mock abm service. Go to `/apps/search/config/app.yml` and go to line 223: set `test_mock_client` to `true`. We will then use the files in `/app/test/abm/data/namedAccounts.json` as response for local ajax requests.

## Patch File

Create patch files:

```bash
svn diff web/mkt-3.0/* > test.patch
```

## Styles

All styles are defined in scss files in `/web/mkt-3.0/resources/sass/`, for example: `/web/mkt-3.0/resources/sass/widgets/_abmDashboard.scss`. We can rewrite the file and run the shell script `/batch/buildCss.sh` to re-build css files.


## Tickets

### LM-98590

* **URL:** https://resource.marketo.com/jira/browse/LM-98590?filter=-1
* **Description:** After deleting the dynamic account list, the left tree doesn't update until the full refresh
* **View:** /web/mkt-3.0/app/view/abm/accountList/DynamicListTree.js
* **Controller:** /web/mkt-3.0/app/controller/abm/accountList/AccountListTree.js

When trying to create new dynamic list, we need some source CRM to name the list. I modified the function `executeCrmViewsAutosuggest` in `apps/search/modules/abm/actions/actions.class.php` to manually add the CRM list. (starting line 2361)

### LM-104697

* **URL:** https://resource.marketo.com/jira/browse/LM-104697?filter=-1
* **Description:** Named Account custom fields can be set without "Edit Named Account" permission
* **View:** /web/mkt-3.0/app/view/abm/namedAccount/CreateForm.js
* **Controller:** /web/mkt-3.0/app/controller/abm/namedAccount/CreateForm.js (Same file name in `controller`)

Starting from line 248 of `/apps/search/lib/data/NamedAccountAccess.php`, modified the code to manually add CRM name to some records.

Deleted the record with ID `1316` in `testBetacust.access_grant`. That is the record for role `1` (admin) and capability `8502` (Edit Named Account). The access level is 100 and access type is `full`.

The data for a named account will be updated via `update` ajax call to the `doUpdate` function in  `/apps/search/lib/data/NamedAccountAccess.php`. However, we can not reach this function since the permission check will be executed in its parent class `DataAccess`.

The response for a 403 http request is `User does not have access`, which is defined in the function `executeForbiddenError` (line 1990) in `/apps/search/modules/user/actions/actions.class.php`. But `executeForbiddenError()` is not called in other files. Actually, it is executed in line 54 in `/apps/search/lib/mktAccessZoneFilter.class.php`:

```php
class mktAccessZoneFilter extends sfFilter {
  ...
  public function execute($filterChain) {
    ...
    // We're authenticated, so any access error goes through user/forbiddenError handler,
    // not the standard user/accessError.
    sfConfig::set('sf_secure_action', 'forbiddenError');
    ...
  }
  ...
}
```
