---
title: 配置仓库的密码扫描
intro: 'You can configure how {% data variables.product.prodname_dotcom %} scans your repositories for secrets that match advanced security patterns.'
product: '{% data reusables.gated-features.secret-scanning %}'
permissions: 'People with admin permissions to a repository can enable {% data variables.product.prodname_secret_scanning_GHAS %} for the repository.'
redirect_from:
  - /github/administering-a-repository/configuring-secret-scanning-for-private-repositories
  - /github/administering-a-repository/configuring-secret-scanning-for-your-repositories
  - /code-security/secret-security/configuring-secret-scanning-for-your-repositories
versions:
  ghes: '*'
  ghae: '*'
  ghec: '*'
type: how_to
topics:
  - Secret scanning
  - Advanced Security
  - Repositories
shortTitle: 配置密钥扫描
---

{% data reusables.secret-scanning.beta %}
{% data reusables.secret-scanning.enterprise-enable-secret-scanning %}

## 启用 {% data variables.product.prodname_secret_scanning_GHAS %}

您可以对组织拥有的任何仓库启用 {% data variables.product.prodname_secret_scanning_GHAS %}。 Once enabled, {% data reusables.secret-scanning.secret-scanning-process %}

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.sidebar-settings %}
{% data reusables.repositories.navigate-to-security-and-analysis %}
4. 如果 {% data variables.product.prodname_advanced_security %} 尚未对仓库启用，请在“{% data variables.product.prodname_GH_advanced_security %}”右侧单击 **Enable（启用）**。
   {% ifversion fpt or ghec %}![为仓库启用 {% data variables.product.prodname_GH_advanced_security %}](/assets/images/help/repository/enable-ghas-dotcom.png)
   {% elsif ghes or ghae %}![Enable {% data variables.product.prodname_GH_advanced_security %} for your repository](/assets/images/enterprise/3.1/help/repository/enable-ghas.png){% endif %}
5. 查看启用 {% data variables.product.prodname_advanced_security %} 的影响，然后点击 **对仓库启用 {% data variables.product.prodname_GH_advanced_security %}**。
6. 当您启用 {% data variables.product.prodname_advanced_security %} 时，{% data variables.product.prodname_secret_scanning %} 可能会因为组织的设置而自动启用。 如果 "{% data variables.product.prodname_secret_scanning_caps %}" 显示 **Enable（启用）**按钮，则您仍需通过单击 **Enable（启用）**来启用 {% data variables.product.prodname_secret_scanning %}。 如果您看到 **Disable（禁用）**按钮，则表明 {% data variables.product.prodname_secret_scanning %} 已启用。 ![为仓库启用 {% data variables.product.prodname_secret_scanning %}](/assets/images/help/repository/enable-secret-scanning-dotcom.png)

{% ifversion ghae %}
1. 在可以启用 {% data variables.product.prodname_secret_scanning %} 之前，您需要先启用 {% data variables.product.prodname_GH_advanced_security %}。 在“{% data variables.product.prodname_GH_advanced_security %}”右边单击 **Enable（启用）**。 ![为仓库启用 {% data variables.product.prodname_GH_advanced_security %}](/assets/images/enterprise/github-ae/repository/enable-ghas-ghae.png)
2. 单击**为此仓库启用 {% data variables.product.prodname_GH_advanced_security %}** 以确认操作。 ![确认为仓库启用 {% data variables.product.prodname_GH_advanced_security %}](/assets/images/enterprise/github-ae/repository/enable-ghas-confirmation-ghae.png)
3. 在“{% data variables.product.prodname_secret_scanning_caps %}”右边单击 **Enable（启用）**。 ![为仓库启用 {% data variables.product.prodname_secret_scanning %}](/assets/images/enterprise/github-ae/repository/enable-secret-scanning-ghae.png)
{% endif %}

## Excluding directories from {% data variables.product.prodname_secret_scanning_GHAS %}

您可以使用 *secret_scanning.yml* 文件从 {% data variables.product.prodname_secret_scanning %} 排除目录。 例如，可以排除包含测试或随机生成内容的目录。

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.files.add-file %}
3. 在文件名字段中，键入 *.github/secret_scanning.yml*。
4. 在 **Edit new file（编辑新文件）**下，键入 `paths-ignore:`，后接您想要从 {% data variables.product.prodname_secret_scanning %} 排除的路径。
    ``` yaml
    paths-ignore:
      - "foo/bar/*.js"
    ```

    您可以使用特殊字符（如 `*`）来过滤路径。 有关过滤模式的更多信息，请参阅“[GitHub Actions 的工作流程语法](/actions/reference/workflow-syntax-for-github-actions#filter-pattern-cheat-sheet)”。

    {% note %}

    **注意：**
    - 如果 `paths-ignore` 中的条目超过 1,000 个，{% data variables.product.prodname_secret_scanning %} 只会从扫描中排除前 1,000 个目录。
    - 如果 *secret_scanning.yml* 大于 1 MB，{% data variables.product.prodname_secret_scanning %} 将忽略整个文件。

    {% endnote %}

您也可以忽略来自 {% data variables.product.prodname_secret_scanning %} 的个别警报。 更多信息请参阅“[管理来自 {% data variables.product.prodname_secret_scanning %} 的警报](/github/administering-a-repository/managing-alerts-from-secret-scanning#managing-secret-scanning-alerts)”。

## 延伸阅读

- “[管理组织的安全性和分析设置](/organizations/keeping-your-organization-secure/managing-security-and-analysis-settings-for-your-organization)”
{% ifversion fpt or ghes > 3.1 or ghae or ghec %}- "[定义 {% data variables.product.prodname_secret_scanning %} 的自定义模式](/code-security/secret-security/defining-custom-patterns-for-secret-scanning)"{% endif %}
