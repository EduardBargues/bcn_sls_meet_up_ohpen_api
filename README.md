# Ohpen-API

How Platform Services Team (PST) created an IDP with on-demand environments and deployments levaraging 100% Serverless technologies in AWS.

# Hello, I'm Eduard Bargués

You can find me on [Github](https://github.com/eduardbargues/), [Linkedin](https://www.linkedin.com/in/eduardbargues/) and [eduardbargues.github.io](https://eduardbargues.github.io/).

I work at [Ohpen](https://ohpen.com) as Platform Owner together with a (small) group of incredible people:

- [Jozef Cajkovic](https://www.linkedin.com/in/jozef-%C4%8Dajkovi%C4%8D-3389b644/) as Cloud Architect and Team Lead.
![josef_image](https://media-exp1.licdn.com/dms/image/C5603AQFKf-Vyb1VGEQ/profile-displayphoto-shrink_800_800/0/1517376141267?e=1663804800&v=beta&t=nKAnpq3N-8jU4Pnhsz5aOyqUCA1mqcFDMbh8MXA8LpE)
- [Matej Liner](https://www.linkedin.com/in/matej-l%C3%ADner-8b283364/) as Cloud Architect.
![matej_image](https://media-exp1.licdn.com/dms/image/C5603AQHUMXScFmYl1w/profile-displayphoto-shrink_800_800/0/1635886638336?e=1663804800&v=beta&t=zYg7OCOqVxgzaB73YVw52jHxHEDMivWdOSuaSRmixiE)
- [Carlos angulo](https://www.linkedin.com/in/angulomascarell/) as DevOps Engineer.
![carlos_image](https://media-exp1.licdn.com/dms/image/C5603AQHvnQy-Og5slQ/profile-displayphoto-shrink_800_800/0/1579111296400?e=1663804800&v=beta&t=MNFeWz9wkTwe6yWe3WGplyyRhXXRGAQVGpoJagLyOgg)

# What was PST born for?

## Ohpen was facing many problems

- Domain teams where exposing apis to clients in (too) many different ways.
- Each new client to onboard had different requirements.
- We had to ensure security and compliance over and over.
- Developers manually maintained their environments.

## The vision

- Self service environments for our developers.
- Automatic creation of environments and apis for our clients.
- Both must be secured the same way as in production.
- Must be easy to use and configure.

# 🛡️ Security

## Auth

- Mutual TLS using Custom Domain Names and AWS certificates manager.
- JWT based access using Cognito, Apigateway and Custom Lambda authorizer.

## IP filtering

IP whitelisting using WAF rules.

# 🧰 Easy integration

## Clients

- Secrets stored in Secrets Manager.
- Only accessible via resource policies and trusted IAM roles.
- Postman collections available.
- All our apis are [publicly documented](https://developer.ohpen.com).

## Developers

- Security first design. They develop exactly like in production.
- They can create/destroy environments and apis via pull requests.

# 👀 Monitoring from day 0

## Compliance

We leverage AWS Config and Cloud Trail to track everything that happens.

## Costs

Creation of Datadog dashboards to monitor everything.

# How does it look?

![]()

## What are developers suposed to do?

# 👏 Success!

## 100+ AWS accounts

## 250+ APIs publicly available

## Everything is 1 pull request away

# Thank you!

[o(h)pen source organization](https://github.com/ohpensource)
[We are hiring!](https://ohpen.pinpointhq.com/)
