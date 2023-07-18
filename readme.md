# wiki on Dokku

```bash
# add upstream
git remote add dokku dokku@weteling.com:wiki


# dokku
dokku apps:create wiki
dokku domains:add wiki wiki.weteling.com wiki.coachcloud.io
dokku letsencrypt:enable wiki
dokku postgres:create wiki-postgres
dokku postgres:link wiki-postgres wiki

dokku proxy:ports-set wiki http:80:3000 https:443:3000



# get this from the pg url

dokku config:set wiki DB_TYPE=postgres DB_HOST=dokku-postgres-wiki-postgres DB_PORT=5432 DB_USER=postgres DB_PASS=XXX DB_NAME=wiki_postgres

```
