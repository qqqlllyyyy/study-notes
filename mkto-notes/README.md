# Marketo Working Notes

## Tickets

Here is a list of ticket notes:

* [December 2017](tickets/2017-12.md)

## Test Files

Since abm service is not setup locally, we can use the test file to mock abm service. Go to `/apps/search/config/app.yml` and go to line 223: set `test_mock_client` to `true`. We will then use the files in `/app/test/abm/data/namedAccounts.json` as response for local ajax requests.

## Work Flow

Create patch files:
```bash
svn diff web/mkt-3.0/* > test.patch
```

Checkin (commit) changes:
```bash
svn commit -m “LM-ticket id some text” file
```

## Styles

All styles are defined in scss files in `/web/mkt-3.0/resources/sass/`, for example: `/web/mkt-3.0/resources/sass/widgets/_abmDashboard.scss`. We can rewrite the file and run the shell script `/batch/buildCss.sh` to re-build css files.
