# Test your Terraform files with Snyk CLI

With Snyk Infrastructure as Code, you can scan both your static configuration files and Terraform plan output using the CLI.

|                                   | **Terraform configuration files** | **Terraform plan file**  |
| --------------------------------- | --------------------------------- | ------------------------ |
| **Identify configuration issues** | Yes                               | Yes                      |
| **Process variables**             | No                                | Yes                      |
| **Scan Terraform modules**        | No                                | Yes - public and private |

## Terraform configuration files

You can scan the configuration files, for example `main.tf`, using the CLI.

External modules are currently not supported.

## Scan configuration files

You can specify either a file name or a whole directory:

```
snyk iac test main.tf
snyk iac test .
```

## Terraform plan

Terraform plan is the step run between writing your configuration files and deploying those changes.

`$ terraform plan` identifies the changes that need to be made to your target environment in order to match your desired state.

As part of this planning stage, all variables and Terraform modules that are used in your targeted Terraform deployment are taken into consideration.

If you have written a custom Terraform module and are referencing it in your deployment, then it is included in the Terraform plan output and scanned accordingly. This means the Terraform plan output provides a complete artifact to be scanned from a security perspective.

As of Snyk CLI version 1.594.0 you can scan this artifact using the Snyk IaC CLI .

This file is not sent to Snyk to be processed; it is scanned locally with the CLI and does not leave your machine.

## Scan Terraform plan output

Provide the path to your Terraform plan output which must be stored as a valid JSON file.

```
snyk iac test tf-plan.json
```

By default, Snyk scans the changes that will be made to your infrastructure, not the full infrastructure.

You can change this behavior by using the `--scan=` option.

* `--scan=resource-changes` is the default behavior. This scans only the changes that would be made to your infrastructure if you ran `$ terraform apply`.
* `--scan=planned-values` scans the full planned state, providing results of the existing infrastructure plus changes that will be made.

If you do not already have your Terraform plan output saved as a JSON file, you may need to follow these steps:

```
terraform plan -out=tfplan.binary
terraform show -json tfplan.binary > tf-plan.json
```

You can name the `tf-plan.json` file according to your needs.

These files are considered sensitive and it is not recommended to commit them to source control.

## Troubleshooting

**There are differences between scanning the static files and plan output**. This may be due to the following:

* **Variables** - Terraform plan output considers the values stored in variables.
* **Terraform modules** - Terraform plan output includes any configuration issues found from Terraform modules that you may be using.
* **Delta** - By default, scanning the Terraform plan output scans only for configuration issues on the changes that will be made, not the whole deployment. In contrast, the static scan looks at all of the files. Try re-running the scan with the `--scan=planned-values` option.

**Note:** The option `--experimental` is not required anymore when testing your Terraform projects.

If you have found a discrepancy that you cannot explain based on this information, submit a request to Support.
