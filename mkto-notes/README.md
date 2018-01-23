# Marketo Working Notes

## Tickets

Here is a list of ticket notes:

* [December 2017](tickets/2017-12.md)
* [January 2018](tickets/2018-01.md)

## Test Files

Since abm service is not setup locally, we can use the test file to mock abm service. Go to `/apps/search/config/app.yml` and go to line 223: set `test_mock_client` to `true`. We will then use the files in `/app/test/abm/data/namedAccounts.json` as response for local ajax requests.

Insert some named account records for abm use: 

```sql
INSERT INTO `mkt_account` (`id`, `name`, `domain_name`, `industry`, `city`, `state`, `country`, `sic_code`, `annual_revenue`, `num_employees`, `is_targeted`, `is_deleted`, `score1`, `score2`, `score3`, `score4`, `score5`, `membership_count`, `oppty_count`, `oppty_amount`, `logo_url`, `created_at`, `updated_at`)
VALUES
	(1,'AnnRev1000',NULL,NULL,NULL,NULL,NULL,NULL,1000,NULL,1,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:04:58','2016-04-18 17:04:58'),
	(2,'AnnRev5',NULL,NULL,NULL,NULL,NULL,NULL,5,NULL,1,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:06:19','2016-04-18 17:06:19'),
	(3,'CityRochester',NULL,NULL,'Rochester',NULL,NULL,NULL,500,NULL,1,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:08:33','2016-04-18 17:08:33'),
	(4,'StateNew',NULL,NULL,NULL,'New Mexico',NULL,NULL,NULL,NULL,1,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:09:51','2016-04-18 17:09:51'),
	(5,'StateNotNew',NULL,NULL,NULL,'California',NULL,NULL,NULL,NULL,1,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:10:10','2016-04-18 17:10:10'),
	(6,'CountryNotEmpty',NULL,NULL,NULL,NULL,'USA',NULL,NULL,NULL,1,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:11:04','2016-04-18 17:11:04'),
	(7,'IndustryWhaling',NULL,'Whaling',NULL,NULL,NULL,NULL,NULL,NULL,1,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:12:00','2016-04-18 17:12:00'),
	(8,'IndustryMining',NULL,'Mining',NULL,NULL,NULL,NULL,NULL,NULL,1,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:12:17','2016-04-18 17:12:17'),
	(9,'IsTargetedFalse',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:13:23','2016-04-18 17:13:23'),
	(10,'NumEmployees50',NULL,NULL,NULL,NULL,NULL,NULL,50,50,1,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:16:14','2016-04-18 17:16:14'),
	(11,'NumEmployees500',NULL,NULL,NULL,NULL,NULL,NULL,NULL,500,1,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:16:26','2016-04-18 17:16:26'),
	(12,'Score1_42',NULL,NULL,'Albany',NULL,NULL,NULL,NULL,NULL,1,0,42,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:17:46','2016-04-18 17:17:46'),
	(13,'Score1_11',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,1,0,11,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:18:54','2016-04-18 17:18:54'),
	(14,'Score2_11',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,1,0,NULL,11,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:19:15','2016-04-18 17:19:15'),
	(15,'Score2_42',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,1,0,NULL,42,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:19:26','2016-04-18 17:19:26'),
	(16,'Score3_42',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,1,0,NULL,NULL,42,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:19:57','2016-04-18 17:19:57'),
	(17,'Score3_50',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,1,0,NULL,NULL,50,NULL,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:20:11','2016-04-18 17:20:11'),
	(18,'Score4_42',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,1,0,NULL,NULL,NULL,42,NULL,NULL,NULL,NULL,NULL,'2016-04-18 17:21:18','2016-04-18 17:21:18'),
	(19,'Score5_42',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,1,0,NULL,NULL,NULL,NULL,42,NULL,NULL,NULL,NULL,'2016-04-18 17:21:44','2016-04-18 17:21:44'),
	(20,'NumPeople28',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,28,NULL,NULL,NULL,'2016-05-05 12:10:35','2016-05-05 12:10:35'),
	(21,'NumPeople5',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,5,NULL,NULL,NULL,'2016-05-05 12:11:11','2016-05-05 12:11:11'),
	(22,'Pipeline20000',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,20000,NULL,'2016-05-05 12:12:30','2016-05-05 12:12:30'),
	(23,'Pipeline500',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,500,NULL,'2016-05-05 12:12:56','2016-05-05 12:12:56'),
	(24,'OpportunityCount1',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,NULL,1,NULL,NULL,'2016-05-05 12:13:35','2016-05-05 12:13:35'),
	(25,'OpportunityCount0',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,NULL,0,NULL,NULL,'2016-05-05 12:13:47','2016-05-05 12:13:47'),
	(26,'IBM-super2','ibm.com',NULL,'Bobville','Bobtucky','Bobland',NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-06-06 16:43:48','2016-06-06 16:43:48'),
	(29,'IBM-super3','ibm.com',NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-06-06 16:54:26','2016-06-06 16:54:26'),
	(34,'IBM-super6','ibm.com',NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-06-07 14:54:08','2016-06-07 14:54:08'),
	(36,'IBM-super7','ibm.com',NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-06-07 17:43:16','2016-06-07 17:43:16'),
	(37,'IBM-super8','ibm.com',NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-06-08 11:40:58','2016-06-08 11:40:58'),
	(39,'IBM-super9','ibm.com',NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-06-08 11:56:31','2016-06-08 11:56:31'),
	(45,'TestAccount_3',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-06-20 11:53:05','2016-06-20 11:53:05'),
	(46,'TestAccount_2',NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,0,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2016-06-20 11:53:06','2016-06-20 11:53:06');
```

## Work Flow

Create patch files:
```bash
svn diff web/mkt-3.0/* > test.patch
```

Checkin (commit) changes:
```bash
svn commit -m “LM-ticket id some text” file
```

Patch to INT test server (check the hostname in browser, `sjintweb1` or `sjintweb2`):

```bash
ssh {{myAccount}}@sjintweb1.marketo.org # Pwd: {{myPwd}}.substring(0, 7)
cd /www/mkto
vi LM-84256.patch # Paste patch diff content here, use ':wq' to save and exit
patch -p0 < LM-84256.patch
php batch/compressScripts.php
# Revert patch:
patch -p0 -R < LM-84256.patch
```

## Styles

All styles are defined in scss files in `/web/mkt-3.0/resources/sass/`, for example: `/web/mkt-3.0/resources/sass/widgets/_abmDashboard.scss`. We can rewrite the file and run the shell script `/batch/buildCss.sh` to re-build css files.

```bash
Install RVM:  
curl -L https://get.rvm.io | bash -s stable --ruby

Install Ruby 1.9.3:
rvm install 1.9.3
rvm use 1.9.3
rvm rubygemslastest
ruby --version

gem list
bigdecimal (1.1.0)
bundler-unload (1.0.2)
chunky_png (1.3.8)
compass (0.12.2)
executable-hooks (1.3.2)
ffi (1.9.18)
fssm (0.2.10)
gem-wrappers (1.3.2)
io-console (0.3)
json (1.5.5)
minitest (2.5.1)
rake (0.9.2.2)
rb-fsevent (0.10.2)
rb-inotify (0.9.10)
rdoc (3.9.5)
rubygems-bundler (1.4.4)

gem install compass -v 0.12.2

sh batch/buildCss.sh
```
