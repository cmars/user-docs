# Code

## Usage

`snyk code [<SUBCOMMAND>] [<OPTIONS>] [<PATH>]`

## Description

The `snyk code` command finds security issues using Static Code Analysis.

For more information see [CLI for Snyk Code](https://docs.snyk.io/snyk-code/cli-for-snyk-code).

## Subcommand: `test`

Test for any known issue.

## Exit codes

Possible exit codes and their meaning:

**0**: success, no vulnerabilities found\
**1**: action\_needed, vulnerabilities found\
**2**: failure, try to re-run command\
**3**: failure, no supported projects detected

## Configure the Snyk CLI

You can use environment variables to configure the Snyk CLI and also set variables to configure the Snyk CLI to connect with the Snyk API. See [Configure the Snyk CLI](https://docs.snyk.io/features/snyk-cli/configure-the-snyk-cli).

## Debug

Use the `-d` option to output the debug logs.

## Options for the code test subcommand

### `--org=<ORG_ID>`

Specify the `<ORG_ID>`to run Snyk commands tied to a specific organization. The `<ORG_ID>` influences private test limits.

If you have multiple organizations, you can set a default from the CLI using:

`$ snyk config set org=<ORG_ID>`

Set a default to ensure all newly tested projects are tested under your default organization. If you need to override the default, use the `--org=<ORG_ID>` option.

Default: `<ORG_ID>` that is the current preferred organization in your [Account settings](https://app.snyk.io/account).

Example: `$ snyk code test --org=my-team`

For more information see the article [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI).

### `--json`

Print results in JSON format.

Example: `$ snyk code test --json-file-output=vuln.json`

### `--sarif`

Return results in SARIF format.

### `--severity-threshold=<low|medium|high|critical>`

Report only vulnerabilities at the specified level or higher. Note that the Snyk Code configuration issues do not currently use the `critical` severity level.
