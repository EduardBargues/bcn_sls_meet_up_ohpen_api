# Serverless IDP within Ohpen

How we created an IDP with on-demand environments leveraging 100% Serverless technologies in AWS.

![idp](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/idp.png)

# Hello, I'm Eduard Bargués

You can find me on:

- [Linkedin](https://www.linkedin.com/in/eduardbargues/).
- [Github](https://github.com/eduardbargues/) or [eduardbargues.github.io](https://eduardbargues.github.io/).

I work at [Ohpen](https://ohpen.com) as Platform Owner together with a group of incredible people.

## Platform Services Team (PST)

![pst_team_png](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/jozef_carlos_matej.png)

- [Jozef Cajkovic](https://www.linkedin.com/in/jozef-%C4%8Dajkovi%C4%8D-3389b644/) as Team Lead and Cloud architect.
- [Matej Liner](https://www.linkedin.com/in/matej-l%C3%ADner-8b283364/) as Cloud Architect.
- [Carlos Angulo](https://www.linkedin.com/in/angulomascarell/) as DevOps Engineer.

## What does Ohpen do?

![ohpen_products](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/ohpen_products.png)

- Provide Saas products to Banks behind APIs.
- Automatically compliant with EU requirements.

# We created APIs in different ways

## Nwk + Stage accounts

![new_stack_setup](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/new_stack_setup.png)

## A more classic approach

![legacy](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/legacy.png)

# This does NOT escale!

![frustation](https://miro.medium.com/max/749/1*BpSFW3UX4JXaBUyasPcx7w.jpeg)

- Managing releases was tedious.
- Security became a stopper instead of being transparent to developers.
- We had to do manual steps to ensure compliance.

## Breath in, breath out

![vision](https://fundhemi.org/wp-content/uploads/2019/03/vision.jpg)

Let's list the requirements and start small.

# Environments

## AWS account setup

## Release management

Something is being deployed.

- Where?
- Which service and version?
- Who is deploying?

# API security

## Mutual TLS

![mtls](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/_mtls.svg)
Using Route53 public Hosted Zones, Custom Domain Names and AWS certificates manager.

## JWT based access

![auth](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/auth.svg)
Using Cognito, Apigateway, Custom Lambda authorizer and Dynamodb.

## IP whitelisting

![waf](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/waf.svg)
Using WAF rules and apigateway.

# Easy integration

## Clients

![secrets](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/secrets.svg)

- Secrets stored in Secrets Manager
- Only accessible via resource policies and trusted IAM roles.
- All our apis are [publickly documented](https://developer.ohpen.com)

## Developers

![devops](https://www.websdirect.es/wp-content/uploads/2022/02/Devops.jpg)

- Security first approach. They develop exactly like in production.
- They can create/destroy environments and apis via pull requests.

# Monitoring

![compliance](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/_datadog.svg)

- AWS Config for compliance and deployment analysis.
- Cost explorer for aggregated reports.
- Cloud Watch for logging.

# How does it look?

![main_diagram](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/main.svg)

# How does it work?

## Pull request to create a new environment

- An "empty" AWS account is created.
- Then, developers add features to it via json configuration.

```json
{
  "account_id": "74...9",
  "defaults": {...},
  "vpc": {...},
  "cloudmap": {...},
  "config": {...}
}
```

TODO: include AVM diagram

## Pull requests to deploy security layer

```hcl
aws_nwk_account_id                       = "5...2"
aws_nwk_deployment_role_name             = "dev-..."
cognito_client_role_trusted_accounts     = ["2...1"]
enable_cognito_client_secrets_collection = true
expose_connection_data_in_ssm            = true
enable_aggregated_datadog_dashboard      = true
waf_allowed_ips = [
  "34.199.54.113/32",
  ...,
  "63.34.100.178/32"
]
```

## Pull requests to deploy api(s)

#### Information about api and environment

```hcl
aws_nwk_account_id           = "8...2"
api = {
  name            = "serverless-template"
  base_path       = "template"
  version         = "1.2.3"
  openapi_version = "3.0.1"
}
```

#### Throttling

```hcl
stage_throttling = {
  enabled = true
  rate    = 1000
  burst   = 100
}
```

#### Endpoints

```hcl
endpoints = {
  "GET /mock" = {
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
}
```

#### Monitoring

```hcl
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

![success](https://assets.entrepreneur.com/content/3x2/2000/20150327221922-success-winning-inspirational.jpeg)

- 100+ AWS accounts.
- 250+ APIs publicly available.
- API deployments under 22 seconds.
- Everything is 1 pull request away.

# Thank you!

![main_diagram](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/main.svg)

- [o(h)pen source organization](https://github.com/ohpensource)
- [We are hiring!](https://ohpen.pinpointhq.com/)
- [Contact me 😄](https://www.linkedin.com/in/eduardbargues/)

Icons from
<a href="https://www.flaticon.com/free-icons/payment" title="payment icons">Payment icons created by Freepik - Flaticon</a>
<a href="https://www.flaticon.com/free-icons/cost" title="cost icons">Cost icons created by Design Circle - Flaticon</a>
<a href="https://www.flaticon.com/free-icons/investment" title="investment icons">Investment icons created by justicon - Flaticon</a>
<a href="https://www.flaticon.com/free-icons/mortgage" title="mortgage icons">Mortgage icons created by RaftelDesign - Flaticon</a>
<a href="https://www.flaticon.com/free-icons/debt" title="debt icons">Debt icons created by Freepik - Flaticon</a>
