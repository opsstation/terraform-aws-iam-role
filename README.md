# terraform-aws-iam-role
[![Latest Release](https://img.shields.io/github/release/opsstation/terraform-aws-vpc-peering.svg)](https://github.com/opsstation/terraform-aws-vpc-peering/releases/latest)
[![tfsec](https://github.com/opsstation/terraform-aws-vpc-peering/actions/workflows/tfsec.yml/badge.svg)](https://github.com/opsstation/terraform-aws-vpc-peering/actions/workflows/tfsec.yml)
[![License](https://img.shields.io/badge/License-APACHE-blue.svg)](LICENSE.md)
[![Changelog](https://img.shields.io/badge/Changelog-blue)](CHANGELOG.md)

---

## 📘 Description

Terraform module to create and manage **AWS VPC Peering Connections** between two VPCs.
This module supports both **intra-account** and **cross-account** peering setups, including automatic route table updates and tagging via the [Labels Module](https://github.com/opsstation/terraform-aws-labels).

---
⚙️ Features

- ✅ Create AWS IAM Roles with customizable policies and trust relationships
- 🔄 Supports assume role policies for services or cross-account access
- 🧩 Integration with Labels Module for consistent resource tagging
- 🔐 Attach managed or inline policies securely
- 📈 Option to enable permissions boundaries for controlled access
- 🧠 Supports role chaining and service-linked roles

## 🚀 Usage Example

```hcl

module "iam-role" {
  source             = "git::https://github.com/opsstation/terraform-aws-iam-role.git?ref=v1.0.0"
  name               = "iam"
  environment        = "test"
  assume_role_policy = data.aws_iam_policy_document.default.json
  policy_enabled     = true
  policy             = data.aws_iam_policy_document.iam-policy.json
}
```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_assume_role_policy"></a> [assume\_role\_policy](#input\_assume\_role\_policy) | Whether to create Iam role. | `any` | n/a | yes |
| <a name="input_description"></a> [description](#input\_description) | The description of the role. | `string` | `""` | no |
| <a name="input_enabled"></a> [enabled](#input\_enabled) | Whether to create Iam role. | `bool` | `true` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | Environment (e.g. `prod`, `dev`, `staging`). | `string` | `""` | no |
| <a name="input_force_detach_policies"></a> [force\_detach\_policies](#input\_force\_detach\_policies) | The policy that grants an entity permission to assume the role. | `bool` | `false` | no |
| <a name="input_label_order"></a> [label\_order](#input\_label\_order) | Label order, e.g. `name`,`application`. | `list(any)` | <pre>[<br>  "name",<br>  "environment"<br>]</pre> | no |
| <a name="input_managed_policy_arns"></a> [managed\_policy\_arns](#input\_managed\_policy\_arns) | Set of exclusive IAM managed policy ARNs to attach to the IAM role | `list(any)` | `[]` | no |
| <a name="input_managedby"></a> [managedby](#input\_managedby) | ManagedBy, eg 'opsstation' | `string` | `""` | no |
| <a name="input_max_session_duration"></a> [max\_session\_duration](#input\_max\_session\_duration) | The maximum session duration (in seconds) that you want to set for the specified role. If you do not specify a value for this setting, the default maximum of one hour is applied. This setting can have a value from 1 hour to 12 hours. | `number` | `3600` | no |
| <a name="input_name"></a> [name](#input\_name) | Name  (e.g. `app` or `cluster`). | `string` | `""` | no |
| <a name="input_path"></a> [path](#input\_path) | The path to the role. | `string` | `"/"` | no |
| <a name="input_permissions_boundary"></a> [permissions\_boundary](#input\_permissions\_boundary) | The ARN of the policy that is used to set the permissions boundary for the role. | `string` | `""` | no |
| <a name="input_policy"></a> [policy](#input\_policy) | The policy document. | `any` | `null` | no |
| <a name="input_policy_arn"></a> [policy\_arn](#input\_policy\_arn) | The ARN of the policy you want to apply. | `string` | `""` | no |
| <a name="input_policy_enabled"></a> [policy\_enabled](#input\_policy\_enabled) | Whether to Attach Iam policy with role. | `bool` | `false` | no |
| <a name="input_repository"></a> [repository](#input\_repository) | Terraform current module repo | `string` | `""` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_arn"></a> [arn](#output\_arn) | Amazon Resource Name (ARN) specifying the role. |
| <a name="output_name"></a> [name](#output\_name) | Name of the role. |
| <a name="output_policy"></a> [policy](#output\_policy) | The policy document attached to the role. |
| <a name="output_role"></a> [role](#output\_role) | The name of the role associated with the policy. |
| <a name="output_tags"></a> [tags](#output\_tags) | A mapping of tags to assign to the resource. |

---
### ☁️ Tag Normalization Rules (AWS)

| Cloud | Case      | Allowed Characters | Example                            |
|--------|-----------|------------------|------------------------------------|
| **AWS** | TitleCase | Any              | `Name`, `Environment`, `CostCenter` |

---

### 💙 Maintained by [OpsStation](https://www.opsstation.com)
> OpsStation — Simplifying Cloud, Securing Scale.