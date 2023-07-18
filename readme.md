# wiki on Dokku

```bash
# add upstream
git remote add dokku dokku@weteling.com:wiki


# dokku
dokku apps:create wiki
dokku domains:add wiki wiki.weteling.com wiki.coachcloud.cc
dokku letsencrypt:enable wiki
dokku postgres:create wiki-postgres
dokku postgres:link wiki-postgres wiki

dokku proxy:ports-set wiki http:80:3000 https:443:3000


dokku config:set wiki wiki_DOMAIN=https://wiki.weteling.com
dokku config:set wiki SECRET_KEY=$(python3 -c "import secrets; print(''.join(secrets.choice([chr(i) for i in range(0x21, 0x7F)]) for i in range(60)));")
dokku run wiki ./manage.py createsuperuser
```
