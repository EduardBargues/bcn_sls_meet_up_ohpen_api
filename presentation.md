# Ohpen-API

How we created an IDP with on-demand environments leveraging 100% Serverless technologies in AWS.

![idp](https://internaldeveloperplatform.org/full_logo.png)

# Hello, I'm Eduard Bargués

You can find me on [Github](https://github.com/eduardbargues/), [Linkedin](https://www.linkedin.com/in/eduardbargues/) and [eduardbargues.github.io](https://eduardbargues.github.io/).

I work at [Ohpen](https://ohpen.com) as Platform Owner together with a (small) group of incredible people:

- [Jozef Cajkovic](https://www.linkedin.com/in/jozef-%C4%8Dajkovi%C4%8D-3389b644/) as Cloud Architect and Team Lead.
![josef_image](https://media-exp1.licdn.com/dms/image/C5603AQFKf-Vyb1VGEQ/profile-displayphoto-shrink_800_800/0/1517376141267?e=1663804800&v=beta&t=nKAnpq3N-8jU4Pnhsz5aOyqUCA1mqcFDMbh8MXA8LpE)
- [Matej Liner](https://www.linkedin.com/in/matej-l%C3%ADner-8b283364/) as Cloud Architect.
![matej_image](https://media-exp1.licdn.com/dms/image/C5603AQHUMXScFmYl1w/profile-displayphoto-shrink_800_800/0/1635886638336?e=1663804800&v=beta&t=zYg7OCOqVxgzaB73YVw52jHxHEDMivWdOSuaSRmixiE)
- [Carlos angulo](https://www.linkedin.com/in/angulomascarell/) as DevOps Engineer.
![carlos_image](https://media-exp1.licdn.com/dms/image/C5603AQHvnQy-Og5slQ/profile-displayphoto-shrink_800_800/0/1579111296400?e=1663804800&v=beta&t=MNFeWz9wkTwe6yWe3WGplyyRhXXRGAQVGpoJagLyOgg)
- [Jakub Stehlík](https://www.linkedin.com/in/jakub-stehl%C3%ADk-a486361b9/) as DevOps Engineer.
![jakub_image](https://media-exp1.licdn.com/dms/image/C5603AQEpxK9SzUTYWA/profile-displayphoto-shrink_800_800/0/1602421908648?e=1664409600&v=beta&t=wkj88fl61MTKyqlX4JcniEKq80tJ6rpznBMJfvDIsTc)

# 👶 The dawn of Platform Services Team

## Ohpen was facing many problems

- Domain teams where exposing apis to clients in (too) many different ways.
- Each new client to onboard had different requirements.
- We had to ensure security and compliance over and over.
- Developers manually maintained their environments.

![frustation](https://miro.medium.com/max/749/1*BpSFW3UX4JXaBUyasPcx7w.jpeg)

## The vision

- Self service environments for our developers.
- On-demand environments and apis for our clients.
- Security first: Everything as in production by default.
- Must be easy to use and configure.

![vision](https://fundhemi.org/wp-content/uploads/2019/03/vision.jpg)

# 🛡️ Security

## Mutual TLS

Using Route53 public Hosted Zones, Custom Domain Names and AWS certificates manager. ![mtls](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/mTLS.svg)

## JWT based access

Using Cognito, Apigateway, Custom Lambda authorizer and Dynamodb. ![jwt](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/jwt_access.svg)

## IP whitelisting

Using WAF rules and apigateway. ![waf](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/waf_ip.svg)

# 🧰 Easy integration

## Clients

#### Secrets stored in Secrets Manager

Only accessible via resource policies and trusted IAM roles.

![secrets](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/_secrets.svg)

#### All our apis are [publicly documented](https://developer.ohpen.com)

## Developers

- Security first approach. They develop exactly like in production.
- They can create/destroy environments and apis via pull requests.

# 👀 Monitoring

- AWS Config for compliance analysis.
- Cost explorer for aggregated reports.
- Cloud Trail to monitor deployments.
- Cloud Watch for logging.

![compliance](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/compliance.svg)

# How does it look?

![main_diagram](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/main.svg)

## How does it work?

#### Pull request to create a new environment

```json
{
  "account_id": "74...9",
  "defaults": {
    ...
  },
  "vpc": {
    ...
  },
  "cloudmap": {
    ...
  },
  "config": {
    ...
  }
}
```

#### Pull requests to deploy security layer

```bash
aws_nwk_account_id                       = "5...2"
aws_nwk_deployment_role_name             = "dev-cicd-automation"
cognito_client_role_trusted_accounts     = ["2...1"]
enable_cognito_client_secrets_collection = true
expose_connection_data_in_ssm            = true
enable_aggregated_datadog_dashboard      = true
waf_allowed_ips = [
  "xx.xx.xx.xxx/32", # Ohpen AWS Client VPN NAT GW IP
  # BITBUCKET IPs
  # https://support.atlassian.com/bitbucket-cloud/docs/what-are-the-bitbucket-cloud-ip-addresses-i-should-use-to-configure-my-corporate-firewall/#Valid-IP-addresses-for-Bitbucket-Pipelines-build-environments
  "34.199.54.113/32",
  "34.232.25.90/32",
  "34.232.119.183/32",
  "34.236.25.177/32",
  "35.171.175.212/32",
  "52.54.90.98/32",
  "52.202.195.162/32",
  "52.203.14.55/32",
  "52.204.96.37/32",
  "34.218.156.209/32",
  "34.218.168.212/32",
  "52.41.219.63/32",
  "35.155.178.254/32",
  "35.160.177.10/32",
  "34.216.18.129/32",
  # DATADOG eu-west-1 IPs
  "63.35.33.198/32",
  "18.200.120.237/32",
  "63.34.100.178/32"
]
```

#### Pull requests to deploy api(s)

```bash
aws_nwk_account_id           = "8...2"
aws_nwk_deployment_role_name = "dev-cicd-automation"
stage_data_trace_enabled     = true
api = {
  name            = "serverless-template"
  base_path       = "template"
  version         = "1.2.3"
  openapi_version = "3.0.1"
}

stage_throttling = {
  enabled = true
  rate    = 1000
  burst   = 100
}

endpoints = {
  "GET /mock-with-no-auth" = {
    integration_type = "MOCK",
    configuration = {
      response_status_code = 200
    }
    auth_type = "NONE"
  }
  "GET /mock-with-cognito-auth-1" = {
    integration_type = "MOCK",
    configuration = {
      response_status_code = 200
    }
    allowed_authorization_scopes = ["ohpen-api-..."]
  }
  "PUT /{id}" = {
    integration_type = "LAMBDA"
    configuration = {
      lambda_function_name = "<your-lambda-function-name>"
    }
    allowed_authorization_scopes = [
      "ohpen-api-..."
    ]
  }
  "GET /http" = {
    integration_type = "HTTP"
    configuration = {
      integration_endpoint_url = "http://EC2...0.eu-west-1.elb.amazonaws.com"
    }
    allowed_authorization_scopes = [
      "ohpen-api-abc-...",
      "ohpen-api-cba-..."
    ]
  }
  "GET /vpc-link" = {
    integration_type = "HTTP"
    configuration = {
      integration_endpoint_url = "http://myApi.example.com"
      vpc_link_id              = "sd...3"
    }
    allowed_authorization_scopes = [
      "ohpen-api-abc-...",
      "ohpen-api-cba-..."
    ]
  },
}

enable_datadog_availability_dashboard = true

enable_datadog_slo = true
datadog_slo_configuration = {
  thresholds = [
    {
      timeframe = "30d"
      target    = 99.9
      warning   = 99.99
    }
  ]
}

enable_datadog_monitors = true
datadog_monitors_configuration = {
  latency = {
    name               = "latency"
    message            = "message @user-name"
    escalation_message = "escalation message @chat-name"
    priority           = 5 # 5(low) -> 1(critical)
    aggregation        = "avg"
    period             = "last_1h"
    metric             = "max:aws.apigateway.latency"
    thresholds = {
      comparison = ">"
      critical   = 29
      warning    = 21
    }
  }
}
```

# 👏 Success!

## 100+ AWS accounts

## 250+ APIs publicly available

## Everything is 1 pull request away

# Thank you!

[o(h)pen source organization](https://github.com/ohpensource)
[We are hiring!](https://ohpen.pinpointhq.com/)
