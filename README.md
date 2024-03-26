# appconfig-agent-local-development-sample

See: https://docs.aws.amazon.com/appconfig/latest/userguide/appconfig-retrieving-simplified-methods-local-development.html

```
$ docker compose up -d

$ curl "http://localhost:2772/applications/Mobile/environments/Development/configurations/EnableMobilePaymentsFeatureFlagConfiguration"
{
  "mobile_payment": {
    "enabled": true,
    "title": "Mobile payments (for orders over $5)"
  },
  "show_stock": {
    "enabled": true
  }
}

$ curl "http://localhost:2772/applications/Mobile/environments/Development/configurations/EnableMobilePaymentsFeatureFlagConfiguration?flag=mobile_payment"
{
    "enabled": true,
    "title": "Mobile payments (for orders over $5)"
  }

$ curl "http://localhost:2772/applications/Mobile/environments/Development/configurations/EnableMobilePaymentsFeatureFlagConfiguration?flag=mobile_payment&flag=show_stock"
{"mobile_payment":{"enabled":true,"title":"Mobile payments (for orders over $5)"},"show_stock":{"enabled":true}}
```
