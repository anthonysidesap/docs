---
title: Sincronizando o uso da licença entre o GitHub Enterprise Server e o GitHub Enterprise Cloud
intro: 'Você pode sincronizar o uso da licença de {% data variables.product.prodname_ghe_server %} com {% data variables.product.prodname_ghe_cloud %} para ver todas as licenças usadas por toda a sua empresa em um só lugar e garantir que as pessoas com contas em ambos os ambientes consomem apenas uma licença de usuário.'
permissions: 'Enterprise owners can sync license usage between enterprise accounts on {% data variables.product.prodname_ghe_server %} and {% data variables.product.prodname_ghe_cloud %}.'
versions:
  ghec: '*'
  ghes: '*'
type: how_to
topics:
  - Enterprise
  - Licensing
shortTitle: Sincronizar uso da licença
---

## Sobre a sincronização do uso da licença

{% data reusables.enterprise-licensing.about-license-sync %}

To ensure that you see up-to-date license details on {% data variables.product.prodname_dotcom_the_website %}, you can sync license usage between the environments automatically, using {% data variables.product.prodname_github_connect %}. For more information about {% data variables.product.prodname_github_connect %}, see "[About {% data variables.product.prodname_github_connect %}]({% ifversion ghec %}/enterprise-server@latest{% endif %}/admin/configuration/configuring-github-connect/about-github-connect){% ifversion ghec %}" in the {% data variables.product.prodname_ghe_server %} documentation.{% elsif ghes %}."{% endif %}

If you don't want to enable {% data variables.product.prodname_github_connect %}, you can manually sync license usage by uploading a file from {% data variables.product.prodname_ghe_server %} to {% data variables.product.prodname_dotcom_the_website %}.

{% data reusables.enterprise-licensing.view-consumed-licenses %}

{% data reusables.enterprise-licensing.verified-domains-license-sync %}

## Sincronizar automaticamente o uso da licença

You can use {% data variables.product.prodname_github_connect %} to automatically synchronize user license count and usage between {% data variables.product.prodname_ghe_server %} and {% data variables.product.prodname_ghe_cloud %}. Para obter mais informações, consulte "[Habilitando a sincronização da licença de usuário para a sua empresa ]({% ifversion ghec %}/enterprise-server@latest{% endif %}/admin/configuration/configuring-github-connect/enabling-automatic-user-license-sync-for-your-enterprise){% ifversion ghec %}" na documentação de {% data variables.product.prodname_ghe_server %}.{% elsif ghes %}."{% endif %}

## Uso da licença sincronizado manualmente

Para sincronizar manualmente o uso das licenças de usuário entre as duas implantações, você pode baixar um arquivo JSON do {% data variables.product.prodname_ghe_server %} e fazer upload desse arquivo no {% data variables.product.prodname_ghe_cloud %}.

{% data reusables.enterprise-accounts.access-enterprise %}
{% data reusables.enterprise-accounts.settings-tab %}
{% data reusables.enterprise-accounts.license-tab %}
5. Em "Quick links" (Links rápidos), para baixar um arquivo com o uso da sua licença atual no {% data variables.product.prodname_ghe_server %}, clique em **Export license usage** (Exportar uso de licença). ![Exportar link de uso de licença](/assets/images/enterprise/business-accounts/export-license-usage-link.png)
{% data reusables.enterprise-accounts.access-enterprise-on-dotcom %}
{% data reusables.enterprise-accounts.settings-tab %}
8. Na barra lateral esquerda, clique em **Enterprise licensing** (Licenciamento Empresarial). ![Aba "Licenciamento empresarial" na barra lateral de configurações da conta corporativa](/assets/images/help/enterprises/enterprise-licensing-tab.png)
{% data reusables.enterprise-accounts.license-tab %}
10. Em "Instâncias Enterprise Server", clique em **Add server usage** (Adicionar uso de servidor). ![Fazer upload do link de uso do GitHub Enterprise Server](/assets/images/help/business-accounts/upload-ghe-server-usage-link.png)
11. Faça upload do arquivo JSON que você baixou do {% data variables.product.prodname_ghe_server %}.![Arrastar e soltar ou selecionar um arquivo para upload](/assets/images/help/business-accounts/upload-ghe-server-usage-file.png)
