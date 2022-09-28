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
- [Carlos Angulo](https://www.linkedin.com/in/angulomascarell/) as DevOps Engineer.
- [Matej Liner](https://www.linkedin.com/in/matej-l%C3%ADner-8b283364/) as Cloud Architect.

## What does Ohpen do?

![ohpen_products](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/ohpen_products.png)

- Provide Saas products to Banks **behind APIs**.
- Automatically secured and compliant with EU requirements.

# How did we manage APIs?

## Multi tenancy supporting many clients

![legacy](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/legacy.png)

## Single tenancy + networking

![new_stack_setup](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/new_stack_setup.png)

## This doesn't escale!

![frustation](https://miro.medium.com/max/749/1*BpSFW3UX4JXaBUyasPcx7w.jpeg)

- Managing releases was tedious.
- Every different setup required compliance and security analysis.
- Customization was the norm.

# The dawn of PST

![vision](https://fundhemi.org/wp-content/uploads/2019/03/vision.jpg)

Let's list the requirements and start small.

## Clients

![customer](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/customer.png)

- Compliance.
- Security.
- Easy integration.

## Release management

![release_management](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/release_management.png)

Something is being deployed.

- Where?
- Which service and version?
- Who is deploying?

## Developers

![developers](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/developers.jpg)

We are developing a new application.

- Focus on bussines.
- Independent deployments.
- Security and compliance must be abstracted.

# AWS accounts

![aws_account_management](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/aws_account_management.png)

## Created via pull request

![dev_pfs_terraform](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/dev_pfs_terraform.png)

## Enriched via `baselines`

![dev_pfs_baseline_conf](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/dev_pfs_baseline_conf.png)

- Developers configure their Aws accounts via pull requests.

## Config baseline

![config_baseline](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/config_baseline.png)

Monitors: Aws **costs**, **compliance** and **deployments**.

![dev_pfs_baseline_terraform](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/dev_pfs_baseline_terraform.png)

## Deployments

![datadog_deployments](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/datadog_deployments.png)

<!-- ## AWS costs -->
<!-- ## Compliance

![datadog_compliance](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/datadog_compliance.png) -->

# What about APIs?

![ohpen_api](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/ohpen_api.png)

## Security

![security](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/security.jpeg)

- mutual TLS.
- JWT based authentication.
- IP whitelisting.

## Monitoring

![datadog_api_dashboard](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/datadog_api_dashboard.png)

## Apis created via pull requests

![ohpen_api_pull_request](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/ohpen_api_pull_request.png)

# 👏 Success!

![success](https://assets.entrepreneur.com/content/3x2/2000/20150327221922-success-winning-inspirational.jpeg)

- 100+ AWS accounts (150+ environments).
- Security and compliants is transparent to developers.
- 250+ APIs publicly available.
- Deployments in seconds.
- Everything is 1 pull request away.
- Open source model to maintain everything.

# Thank you!

![main_diagram](https://raw.githubusercontent.com/EduardBargues/bcn_sls_meet_up_ohpen_api/main/images/main_diagram.png)

- [o(h)pen source organization](https://github.com/ohpensource)
- [We are hiring!](https://ohpen.pinpointhq.com/)
- [Contact me 😄](https://www.linkedin.com/in/eduardbargues/)

Icons from
<a href="https://www.flaticon.com/free-icons/payment" title="payment icons">Payment icons created by Freepik - Flaticon</a>
<a href="https://www.flaticon.com/free-icons/cost" title="cost icons">Cost icons created by Design Circle - Flaticon</a>
<a href="https://www.flaticon.com/free-icons/investment" title="investment icons">Investment icons created by justicon - Flaticon</a>
<a href="https://www.flaticon.com/free-icons/mortgage" title="mortgage icons">Mortgage icons created by RaftelDesign - Flaticon</a>
<a href="https://www.flaticon.com/free-icons/debt" title="debt icons">Debt icons created by Freepik - Flaticon</a>
<a href="https://www.flaticon.com/free-icons/close" title="close icons">Close icons created by Pixel perfect - Flaticon</a>
