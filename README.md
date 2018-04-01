# terraform-aws-kops-external-dns [![Build Status](https://travis-ci.org/cloudposse/terraform-aws-kops-external-dns.svg?branch=master)](https://travis-ci.org/cloudposse/terraform-aws-kops-external-dns)

Terraform module to provision an IAM role for `external-dns` running in a Kops cluster, and attach an IAM policy to the role with permissions to modify Route53 record sets.


## Overview

This module assumes you are running [external-dns](https://github.com/kubernetes-incubator/external-dns) in a Kops cluster.

It will provision an IAM role with the required permissions and grant the k8s masters the permission to assume it.

This is useful to make Kubernetes services discoverable via AWS DNS services.

The module uses [terraform-aws-kops-metadata](https://github.com/cloudposse/terraform-aws-kops-metadata) to lookup resources within a Kops cluster for easier integration with Terraform.


## Usage

```hcl
module "kops_external_dns" {
  source       = "git::https://github.com/cloudposse/terraform-aws-kops-external-dns.git?ref=master"
  namespace    = "cp"
  stage        = "prod"
  name         = "domain.com"
  masters_name = "masters"

  tags = {
    Cluster = "k8s.domain.com"
  }
}
```


## Variables

|  Name              |  Default     |  Description                                                                     | Required |
|:-------------------|:-------------|:---------------------------------------------------------------------------------|:--------:|
| `namespace`        | ``           | Namespace (_e.g._ `cp` or `cloudposse`)                                          | Yes      |
| `stage`            | ``           | Stage (_e.g._ `prod`, `dev`, `staging`)                                          | Yes      |
| `name`             | ``           | Name of the Kops DNS zone (e.g. `domain.com`)                                    | Yes      |
| `attributes`       | `[]`         | Additional attributes (_e.g._ `policy` or `role`)                                | No       |
| `tags`             | `{}`         | Additional tags  (_e.g._ `map("Cluster","k8s.domain.com")`                       | No       |
| `delimiter`        | `-`          | Delimiter to be used between `namespace`, `stage`, `name`, and `attributes`      | No       |
| `masters_name`     | `masters`    | k8s masters subdomain name in the Kops DNS zone                                  | No       |


## Outputs

| Name               | Description          |
|:-------------------|:---------------------|
| `role_name`        | IAM role name        |
| `role_unique_id`   | IAM role unique ID   |
| `role_arn`         | IAM role ARN         |
| `policy_name`      | IAM policy name      |
| `policy_id`        | IAM policy ID        |
| `policy_arn`       | IAM policy ARN       |


## Help

**Got a question?**

File a GitHub [issue](https://github.com/cloudposse/terraform-aws-kops-external-dns/issues), send us an [email](mailto:hello@cloudposse.com) or reach out to us on [Gitter](https://gitter.im/cloudposse/).


## Contributing

### Bug Reports & Feature Requests

Please use the [issue tracker](https://github.com/cloudposse/terraform-aws-kops-external-dns/issues) to report any bugs or file feature requests.

### Developing

If you are interested in being a contributor and want to get involved in developing `terraform-aws-kops-external-dns`, we would love to hear from you! Shoot us an [email](mailto:hello@cloudposse.com).

In general, PRs are welcome. We follow the typical "fork-and-pull" Git workflow.

 1. **Fork** the repo on GitHub
 2. **Clone** the project to your own machine
 3. **Commit** changes to your own branch
 4. **Push** your work back up to your fork
 5. Submit a **Pull request** so that we can review your changes

**NOTE:** Be sure to merge the latest from "upstream" before making a pull request!


## License

[APACHE 2.0](LICENSE) © 2018 [Cloud Posse, LLC](https://cloudposse.com)

See [LICENSE](LICENSE) for full details.

    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.


## About

`terraform-aws-kops-external-dns` is maintained and funded by [Cloud Posse, LLC][website].

![Cloud Posse](https://cloudposse.com/logo-300x69.png)


Like it? Please let us know at <hello@cloudposse.com>

We love [Open Source Software](https://github.com/cloudposse/)!

See [our other projects][community]
or [hire us][hire] to help build your next cloud platform.

  [website]: https://cloudposse.com/
  [community]: https://github.com/cloudposse/
  [hire]: https://cloudposse.com/contact/


## Contributors

| [![Erik Osterman][erik_img]][erik_web]<br/>[Erik Osterman][erik_web] | [![Andriy Knysh][andriy_img]][andriy_web]<br/>[Andriy Knysh][andriy_web] |[![Igor Rodionov][igor_img]][igor_web]<br/>[Igor Rodionov][igor_img]
|-------------------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|

[erik_img]: http://s.gravatar.com/avatar/88c480d4f73b813904e00a5695a454cb?s=144
[erik_web]: https://github.com/osterman/
[andriy_img]: https://avatars0.githubusercontent.com/u/7356997?v=4&u=ed9ce1c9151d552d985bdf5546772e14ef7ab617&s=144
[andriy_web]: https://github.com/aknysh/
[igor_img]: http://s.gravatar.com/avatar/bc70834d32ed4517568a1feb0b9be7e2?s=144
[igor_web]: https://github.com/goruha/
