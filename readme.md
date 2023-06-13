# GlitchTip on Dokku

```bash
# add upstream
git remote add dokku weteling.com:glitchtip


# dokku
dokku apps:create glitchtip
dokku postgres:create glitchtip-postgres
dokku postgres:link glitchtip-postgres glitchtip
dokku redis:create glitchtip-redis
dokku redis:link glitchtip-redis glitchtip

dokku ps:scale glitchtip worker=1
dokku proxy:ports-set glitchtip http:80:8080 https:443:8080
dokku config:set glitchtip GLITCHTIP_DOMAIN=https://glitchtip.dokku.me
dokku config:set glitchtip SECRET_KEY=$(python3 -c "import secrets; print(''.join(secrets.choice([chr(i) for i in range(0x21, 0x7F)]) for i in range(60)));")
dokku run glitchtip ./manage.py createsuperuser
```

Refer to the [GlitchTip Configuration documentation](https://glitchtip.com/documentation/install#configuration) for other variables you can set such as for e-mail notifications, etc.

### Start using GlitchTip!

You're now fully set up to use GlitchTip! Go to the address you've set for your GlitchTip app and log in with your superuser to get started!

## References

- [GlitchTip's Configuration Documentation](https://glitchtip.com/documentation/install#configuration)
- [GlitchTip's meta repo on self-hosting on Heroku and DigitalOcean App Platform](https://gitlab.com/glitchtip/glitchtip)
