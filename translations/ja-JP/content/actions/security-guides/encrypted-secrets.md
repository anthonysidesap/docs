---
title: 暗号化されたシークレット
intro: 'Encrypted secrets allow you to store sensitive information in your organization{% ifversion fpt or ghes or ghec %}, repository, or repository environments{% else %} or repository{% endif %}.'
redirect_from:
  - /github/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets
  - /actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets
  - /actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets
  - /actions/configuring-and-managing-workflows/using-variables-and-secrets-in-a-workflow
  - /actions/reference/encrypted-secrets
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
---

{% data reusables.actions.enterprise-beta %}
{% data reusables.actions.enterprise-github-hosted-runners %}

## 暗号化されたシークレットについて

Secrets are encrypted environment variables that you create in an organization, repository, or repository environment. 作成したシークレットは、{% data variables.product.prodname_actions %}ワークフローで利用できます。 {% data variables.product.prodname_dotcom %}はシークレットが{% data variables.product.prodname_dotcom %}に到達する前に暗号化され、ワークフローで使用されるまで暗号化されたままになっていることを確実にするのを助けるために[libsodium sealed box](https://libsodium.gitbook.io/doc/public-key_cryptography/sealed_boxes)を使います。

{% data reusables.actions.secrets-org-level-overview %}

環境レベルで保存されたシークレットについては、それらへのアクセスを制御するために必須のレビュー担当者を有効化することができます。 必須の承認者によって許可されるまで、ワークフローのジョブは環境のシークレットにアクセスできません。

{% ifversion fpt or ghec or ghae-issue-4856 %}

{% note %}

**注釈**: {% data reusables.actions.about-oidc-short-overview %}

{% endnote %}

{% endif %}

### シークレットに名前を付ける

{% data reusables.codespaces.secrets-naming %}

  For example, a secret created at the environment level must have a unique name in that environment, a secret created at the repository level must have a unique name in that repository, and a secret created at the organization level must have a unique name at that level.

  {% data reusables.codespaces.secret-precedence %} Similarly, if an organization, repository, and environment all have a secret with the same name, the environment-level secret takes precedence.

{% data variables.product.prodname_dotcom %} がログのシークレットを確実に削除するよう、シークレットの値として構造化データを使用しないでください。 たとえば、JSONやエンコードされたGit blobを含むシークレットは作成しないでください。

### シークレットにアクセスする

シークレットをアクションが使用できるようにするには、ワークフローファイルでシークレットを入力または環境変数に設定する必要があります。 アクションに必要な入力および環境変数については、アクションのREADMEファイルを確認します。 詳しい情報については、「[{% data variables.product.prodname_actions %}のワークフロー構文](/articles/workflow-syntax-for-github-actions/#jobsjob_idstepsenv)」を参照してください。

ファイルを編集するアクセス権を持っていれば、ワークフローファイル中の暗号化されたシークレットを使い、読み取ることができます。 詳細は「[{% data variables.product.prodname_dotcom %} 上のアクセス権限](/github/getting-started-with-github/access-permissions-on-github)」を参照してください。

{% data reusables.actions.secrets-redaction-warning %}

Organization及びリポジトリのシークレットはワークフローの実行がキューイングされた時点で読まれ、環境のシークレットは環境を参照しているジョブが開始された時点で読まれます。

REST API を使用してシークレットを管理することもできます。 For more information, see "[Secrets](/rest/reference/actions#secrets)."

### 認証情報のアクセス許可を制限する

クレデンシャルを生成する際には、可能な限り最小限の権限だけを許可することをおすすめします。 たとえば、個人の認証情報を使う代わりに、[デプロイキー](/developers/overview/managing-deploy-keys#deploy-keys)あるいはサービスアカウントを使ってください。 必要なのが読み取りだけであれば、読み取りのみの権限を許可すること、そしてアクセスをできるかぎり限定することを考慮してください。 個人アクセストークン（PAT）を生成する際には、必要最小限のスコープを選択してください。

{% note %}

**Note:** You can use the REST API to manage secrets. 詳しい情報については「[{% data variables.product.prodname_actions %}シークレットAPI](/rest/reference/actions#secrets)」を参照してください。

{% endnote %}

## リポジトリに暗号化されたシークレットを作成する

{% data reusables.actions.permissions-statement-secrets-repository %}

{% webui %}

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.sidebar-settings %}
{% data reusables.actions.sidebar-secret %}
1. **New repository secret（新しいリポジトリのシークレット）**をクリックしてください。
1. **[Name（名前）]** 入力ボックスにシークレットの名前を入力します。
1. シークレットの値を入力します。
1. [**Add secret（シークレットの追加）**] をクリックします。

If your repository has environment secrets or can access secrets from the parent organization, then those secrets are also listed on this page.

{% endwebui %}

{% cli %}

{% data reusables.cli.cli-learn-more %}

To add a repository secret, use the `gh secret set` subcommand. Replace `secret-name` with the name of your secret.

```shell
gh secret set <em>secret-name</em>
```

The CLI will prompt you to enter a secret value. Alternatively, you can read the value of the secret from a file.

```shell
gh secret set <em>secret-name</em> < secret.txt
```

To list all secrets for the repository, use the `gh secret list` subcommand.

{% endcli %}

## 環境の暗号化されたシークレットの生成

{% data reusables.actions.permissions-statement-secrets-environment %}

{% webui %}

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.sidebar-settings %}
{% data reusables.actions.sidebar-environment %}
1. シークレットを追加したい環境をクリックしてください。
2. **Environment secrets（環境のシークレット）**の下で、**Add secret（シークレットの追加）**をクリックしてください。
3. **[Name（名前）]** 入力ボックスにシークレットの名前を入力します。
4. シークレットの値を入力します。
5. [**Add secret（シークレットの追加）**] をクリックします。

{% endwebui %}

{% cli %}

To add a secret for an environment, use the `gh secret set` subcommand with the `--env` or `-e` flag followed by the environment name.

```shell
gh secret set --env <em>environment-name</em> <em>secret-name</em>
```

To list all secrets for an environment, use the `gh secret list` subcommand with the `--env` or `-e` flag followed by the environment name.

```shell
gh secret list --env <em>environment-name</em>
```

{% endcli %}

## Organizationの暗号化されたシークレットの作成

Organizationでシークレットを作成する場合、ポリシーを使用して、そのシークレットにアクセスできるリポジトリを制限できます。 たとえば、すべてのリポジトリにアクセスを許可したり、プライベート リポジトリまたは指定したリポジトリ のリストのみにアクセスを制限したりできます。

{% data reusables.actions.permissions-statement-secrets-organization %}

{% webui %}

{% data reusables.organizations.navigate-to-org %}
{% data reusables.organizations.org_settings %}
{% data reusables.actions.sidebar-secret %}
1. **New organization secret（新しいOrganizationのシークレット）**をクリックしてください。
1. **[Name（名前）]** 入力ボックスにシークレットの名前を入力します。
1. シークレットの **Value（値）** を入力します。
1. [ **Repository access（リポジトリアクセス）** ドロップダウン リストから、アクセス ポリシーを選択します。
1. [**Add secret（シークレットの追加）**] をクリックします。

{% endwebui %}

{% cli %}

{% note %}

**Note:** By default, {% data variables.product.prodname_cli %} authenticates with the `repo` and `read:org` scopes. To manage organization secrets, you must additionally authorize the `admin:org` scope.

```
gh auth login --scopes "admin:org"
```

{% endnote %}

To add a secret for an organization, use the `gh secret set` subcommand with the `--org` or `-o` flag followed by the organization name.

```shell
gh secret set --org <em>organization-name</em> <em>secret-name</em>
```

By default, the secret is only available to private repositories. To specify that the secret should be available to all repositories within the organization, use the `--visibility` or `-v` flag.

```shell
gh secret set --org <em>organization-name</em> <em>secret-name</em> --visibility all
```

To specify that the secret should be available to selected repositories within the organization, use the `--repos` or `-r` flag.

```shell
gh secret set --org <em>organization-name</em> <em>secret-name</em> --repos <em>repo-name-1</em>,<em>repo-name-2</em>"
```

To list all secrets for an organization, use the `gh secret list` subcommand with the `--org` or `-o` flag followed by the organization name.

```shell
gh secret list --org <em>organization-name</em>
```

{% endcli %}

## Organizationレベルのシークレットへのアクセスの確認

Organization内のシークレットに適用されているアクセス ポリシーを確認できます。

{% data reusables.organizations.navigate-to-org %}
{% data reusables.organizations.org_settings %}
{% data reusables.actions.sidebar-secret %}
1. シークレットのリストには、設定済みのアクセス許可とポリシーが含まれます。 例: ![シークレットリスト](/assets/images/help/settings/actions-org-secrets-list.png)
1. 各シークレットに設定されているアクセス許可の詳細については、[**Update（更新）**] をクリックしてください。

## 暗号化されたシークレットのワークフロー内での利用

{% note %}

**Note:** {% data reusables.actions.forked-secrets %}

{% endnote %}

アクションに入力あるいは環境変数としてシークレットを提供するには、リポジトリ内に作成したシークレットにアクセスする`secrets`コンテキストを使うことができます。 For more information, see "[Contexts](/actions/learn-github-actions/contexts)" and "[Workflow syntax for {% data variables.product.prodname_actions %}](/github/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions)."

{% raw %}
```yaml
steps:
  - name: Hello world action
    with: # Set the secret as an input
      super_secret: ${{ secrets.SuperSecret }}
    env: # Or as an environment variable
      super_secret: ${{ secrets.SuperSecret }}
```
{% endraw %}

可能であれば、コマンドラインからプロセス間でシークレットを渡すのは避けてください。 Command-line processes may be visible to other users (using the `ps` command) or captured by [security audit events](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/command-line-process-auditing). シークレットの保護のために、環境変数、`STDIN`、あるいはターゲットのプロセスがサポートしている他の仕組みの利用を考慮してください。

コマンドラインからシークレットを渡さなければならない場合は、それらを適切なルールでクオート内に収めてください。 シークレットは、意図せずシェルに影響するかもしれない特殊なキャラクターをしばしば含みます。 それらの特殊なキャラクターをエスケープするには、環境変数をクオートで囲ってください。 例:

### Bashの利用例

{% raw %}
```yaml
steps:
  - shell: bash
    env:
      SUPER_SECRET: ${{ secrets.SuperSecret }}
    run: |
      example-command "$SUPER_SECRET"
```
{% endraw %}

### PowerShellの利用例

{% raw %}
```yaml
steps:
  - shell: pwsh
    env:
      SUPER_SECRET: ${{ secrets.SuperSecret }}
    run: |
      example-command "$env:SUPER_SECRET"
```
{% endraw %}

### Cmd.exeの利用例

{% raw %}
```yaml
steps:
  - shell: cmd
    env:
      SUPER_SECRET: ${{ secrets.SuperSecret }}
    run: |
      example-command "%SUPER_SECRET%"
```
{% endraw %}

## シークレットの制限

You can store up to 1,000 organization secrets, 100 repository secrets, and 100 environment secrets.

A workflow created in a repository can access the following number of secrets:

* All 100 repository secrets.
* If the repository is assigned access to more than 100 organization secrets, the workflow can only use the first 100 organization secrets (sorted alphabetically by secret name).
* All 100 environment secrets.

シークレットの容量は最大64 KBです。 64 KBより大きなシークレットを使うには、暗号化されたシークレットをリポジトリ内に保存して、復号化パスフレーズを{% data variables.product.prodname_dotcom %}に保存します。 たとえば、{% data variables.product.prodname_dotcom %}のリポジトリにファイルをチェックインする前に、`gpg`を使って認証情報をローカルで暗号化します。 詳しい情報については、「[gpg manpage](https://www.gnupg.org/gph/de/manual/r1023.html)」を参照してください。

{% warning %}

**警告**: アクションを実行する際、シークレットが出力されないよう注意してください。 この回避策を用いる場合、{% data variables.product.prodname_dotcom %}はログに出力されたシークレットを削除しません。

{% endwarning %}

1. ターミナルから以下のコマンドを実行して、`gpg`およびAES256暗号アルゴリズムを使用して`my_secret.json`ファイルを暗号化します。

 ``` shell
 $ gpg --symmetric --cipher-algo AES256 my_secret.json
 ```

1. パスフレーズを入力するよう求められます。 このパスフレーズを覚えておいてください。{% data variables.product.prodname_dotcom %}で、このパスフレーズを値として用いる新しいシークレットを作成するために必要になります。

1. パスフレーズを含む新しいシークレットを作成します。 たとえば、`LARGE_SECRET_PASSPHRASE`という名前で新しいシークレットを作成し、シークレットの値を上記のステップで選択したパスフレーズに設定します。

1. 暗号化したファイルをリポジトリ内にコピーしてコミットします。 この例では、暗号化したファイルは`my_secret.json.gpg`です。

1. パスワードを復号化するシェルスクリプトを作成します。 このファイルを`decrypt_secret.sh`として保存します。

  ``` shell
  #!/bin/sh

  # ファイルを復号化
  mkdir $HOME/secrets
  # --batchでインタラクティブなコマンドを防ぎ、
  # --yes で質問に対して "はい" が返るようにする
  gpg --quiet --batch --yes --decrypt --passphrase="$LARGE_SECRET_PASSPHRASE" \
  --output $HOME/secrets/my_secret.json my_secret.json.gpg
  ```

1. リポジトリにチェックインする前に、シェルスクリプトが実行可能であることを確かめてください。

  ``` shell
  $ chmod +x decrypt_secret.sh
  $ git add decrypt_secret.sh
  $ git commit -m "Add new decryption script"
  $ git push
  ```

1. ワークフローから、`step`を使用してシェルスクリプトを呼び出し、シークレットを復号化します。 ワークフローを実行している環境にリポジトリのコピーを作成するには、[`actions/checkout`](https://github.com/actions/checkout)アクションを使用する必要があります。 リポジトリのルートを基準として`run`コマンドを使用し、シェルスクリプトを参照します。

{% raw %}
  ```yaml
  name: Workflows with large secrets

  on: push

  jobs:
    my-job:
      name: My Job
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v2
        - name: Decrypt large secret
          run: ./.github/scripts/decrypt_secret.sh
          env:
            LARGE_SECRET_PASSPHRASE: ${{ secrets.LARGE_SECRET_PASSPHRASE }}
        # このコマンドは、あなたの秘密が印刷されていることを示す例
        # シークレットを出力する文は必ず削除してください。 GitHub does
        # not hide secrets that use this workaround.
        - name: Test printing your secret (Remove this step in production)
          run: cat $HOME/secrets/my_secret.json
  ```
{% endraw %}

## Storing Base64 binary blobs as secrets

You can use Base64 encoding to store small binary blobs as secrets. You can then reference the secret in your workflow and decode it for use on the runner. For the size limits, see ["Limits for secrets"](/actions/security-guides/encrypted-secrets#limits-for-secrets).

{% note %}

**Note**: Note that Base64 only converts binary to text, and is not a substitute for actual encryption.

{% endnote %}

1. Use `base64` to encode your file into a Base64 string. 例:

   ```
   $ base64 -i cert.der -o cert.base64
   ```

1. Create a secret that contains the Base64 string. 例:

   ```
   $ gh secret set CERTIFICATE_BASE64 < cert.base64
   ✓ Set secret CERTIFICATE_BASE64 for octocat/octorepo
   ```

1. To access the Base64 string from your runner, pipe the secret to `base64 --decode`.  例:

   ```yaml
   name: Retrieve Base64 secret
   on:
     push:
       branches: [ octo-branch ]
   jobs:
     decode-secret:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v2
         - name: Retrieve the secret and decode it to a file
           env:
             {% raw %}CERTIFICATE_BASE64: ${{ secrets.CERTIFICATE_BASE64 }}{% endraw %}
           run: |
             echo $CERTIFICATE_BASE64 | base64 --decode > cert.der
         - name: Show certificate information
           run: |
             openssl x509 -in cert.der -inform DER -text -noout
   ```

