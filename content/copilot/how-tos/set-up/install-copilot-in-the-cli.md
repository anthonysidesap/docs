---
title: Installing GitHub Copilot in the CLI
intro: 'Learn how to install {% data variables.copilot.copilot_cli_short %} so that you can get suggestions and explanations for the command line.'
versions:
  feature: copilot-in-the-cli
topics:
  - Copilot
  - CLI
shortTitle: Install Copilot in the CLI
redirect_from:
  - /copilot/github-copilot-in-the-cli/enabling-github-copilot-in-the-cli
  - /copilot/github-copilot-in-the-cli/setting-up-github-copilot-in-the-cli
  - /copilot/github-copilot-in-the-cli/installing-github-copilot-in-the-cli
  - /copilot/managing-copilot/configure-personal-settings/installing-github-copilot-in-the-cli
  - /copilot/how-tos/personal-settings/installing-github-copilot-in-the-cli
  - /copilot/how-tos/set-up/installing-github-copilot-in-the-cli
contentType: how-tos
---

## Prerequisites

* **Access to {% data variables.product.prodname_copilot %}**. See [AUTOTITLE](/copilot/about-github-copilot/what-is-github-copilot#getting-access-to-copilot).
* **{% data variables.product.prodname_cli %} installed.** {% data reusables.cli.cli-installation %}

If you have access to {% data variables.product.prodname_copilot %} via your organization or enterprise, you cannot use {% data variables.copilot.copilot_cli_short %} if your organization owner or enterprise administrator has disabled {% data variables.copilot.copilot_cli_short %}. See [AUTOTITLE](/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-github-copilot-features-in-your-organization/managing-policies-for-copilot-in-your-organization).

## Installing {% data variables.copilot.copilot_cli_short %}

1. If you have not already authenticated to the {% data variables.product.prodname_cli %}, run the following command in your terminal.

   ```shell copy
   gh auth login
   ```

1. To install the {% data variables.copilot.copilot_cli_short %} extension, run the following command.

   ```shell copy
   gh extension install github/gh-copilot
   ```

## Updating {% data variables.copilot.copilot_cli_short %}

After installing the {% data variables.copilot.copilot_cli_short %} extension, you can update at any time by running:

```shell copy
gh extension upgrade gh-copilot
```

## Further reading

* [AUTOTITLE](/copilot/github-copilot-in-the-cli/using-github-copilot-in-the-cli)
* [AUTOTITLE](/copilot/github-copilot-in-the-cli/configuring-github-copilot-in-the-cli)
