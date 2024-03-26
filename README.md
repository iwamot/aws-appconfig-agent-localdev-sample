# aws-appconfig-agent-localdev-sample

A sample for local development using the AWS AppConfig Agent.

See: https://docs.aws.amazon.com/appconfig/latest/userguide/appconfig-retrieving-simplified-methods-local-development.html

## Retrieving configuration data

```
$ docker compose up -d

$ curl "http://localhost:2772/applications/myapp/environments/myenv/configurations/myconf"
{
  "featureA": {
    "enabled": true
  },
  "featureB": {
    "enabled": false
  },
  "featureC": true
}

$ curl "http://localhost:2772/applications/myapp/environments/myenv/configurations/myconf?flag=featureA"
{
    "enabled": true
  }

$ curl "http://localhost:2772/applications/myapp/environments/myenv/configurations/myconf?flag=featureA&flag=featureB"
{"featureA":{"enabled":true},"featureB":{"enabled":false}}

$ curl "http://localhost:2772/applications/myapp/environments/myenv/configurations/myconf?flag=featureC"
{"Details":{"Value":{"featureC":{"Problem":"NoSuchFlag"}}},"Message":"Configuration data missing one or more flag values","Reason":"InvalidParameters"}
```

## Updating and validating configuration data

```
$ jq '.featureB.enabled = true' local_configs/myapp\:myenv\:myconf.json > tmp.json && mv tmp.json local_configs/myapp\:myenv\:myconf.json

$ sleep 45

$ curl "http://localhost:2772/applications/myapp/environments/myenv/configurations/myconf?flag=featureB"
{
    "enabled": true
  }
```
