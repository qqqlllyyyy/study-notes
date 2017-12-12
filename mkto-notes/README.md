
## Database

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

#### LM-104697

* **URL:** https://resource.marketo.com/jira/browse/LM-104697?filter=-1
* **Description:** Named Account custom fields can be set without "Edit Named Account" permission
* **View:** /web/mkt-3.0/app/view/abm/namedAccount/CreateForm.js
* **Controller:** /web/mkt-3.0/app/controller/abm/namedAccount/CreateForm.js (Same file name in `controller`)

Starting from line 248 of `/apps/search/lib/data/NamedAccountAccess.php`, modified the code to manually add CRM name to some records.

#### LM-98590

* **URL:** https://resource.marketo.com/jira/browse/LM-98590?filter=-1
* **Description:** After deleting the dynamic account list, the left tree doesn't update until the full refresh
* **View:** /web/mkt-3.0/app/view/abm/accountList/DynamicListTree.js
* **Controller:** /web/mkt-3.0/app/controller/abm/accountList/AccountListTree.js

When trying to create new dynamic list, we need some source CRM to name the list. I modified the function `executeCrmViewsAutosuggest` in `apps/search/modules/abm/actions/actions.class.php` to manually add the CRM list.
