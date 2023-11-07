# VPM 包列表模板

用于制作您自己的包列表的入门工具，包括构建和发布它们的自动化。

完成所有设置后，您将能够更新“source.json”文件，并生成一个在 VPM 中工作的列表，用于为所有列出的包提供更新。

## ▶ 开始使用

* 按 [![使用此模板](https://user-images.githubusercontent.com/737888/185467681-e5fdb099-d99f-454b-8d9e-0760e5a6e588.png)]([https://github.com/vrchat- 社区/模板包列表/生成](https://github.com/mmyo456/template-package-listing/generate)）
基于此模板启动一个新的 GitHub 项目，然后按照其中的说明进行操作。
   * 选择合适的存储库名称和描述。
   * 将可见性设置为“公开”。 您还可以选择“私人”并稍后更改。
   * 您不需要选择“包括所有分支”。
* 在 Web 浏览器中编辑 GitHub 上的此项目，或使用 Git 将其克隆到本地存储库。
   * 如果您不熟悉 Git 和 GitHub，[访问 GitHub 的文档](https://docs.github.com/en/get-started/quickstart/
  
## 设置自动化

您需要编辑此模板中的一些文件，从 [`source.json`](source.json) 开始：
- 填写有关您列表的一般信息，例如“名称”、“id”、“作者”、“描述”等。
- 确保更新第 4 行的“url”字段，将“vrchat-community”替换为您的 GitHub 用户名，将“template-package-listing”替换为您的存储库名称。 该链接将用于在 GitHub 发布您的列表后下载您的列表。 例如，创建名为“thupper-listing”的存储库的用户“thupper”会将 url 更新为“https://thupper.github.io/thupper-listing/index.json”。
- 使用您创建的新存储库的 url 更新“infoLink”（第 11 行）中的“url”。
- 如果您想包含托管在 GitHub 上的包，请在 `githubRepos` 中指定它们。
- 如果您想将在其他地方托管的包包含为“.zip”文件，请在“packages”中指定它们。
   - 如果您不使用`githubRepos`或`packages`，您可以安全地删除它们。
- 最后，转到存储库的“设置”页面，然后选择“页面”，然后查找标题“构建和部署”。 将“源”下拉列表从“从分支部署”更改为“GitHub Actions”。

## 📃 重建列表

每当您对“main”分支进行更改或手动触发它时，“构建存储库列表”操作都会为所有可用版本创建一个新索引，并将它们发布为在 GitHub Pages 上免费托管的网站。 VPM 可以使用此列表来使您的软件包保持最新状态，并且生成的索引页面可以用作包含软件包信息的简单登录页面。 您的包的 URL 格式为 https://username.github.io/repo-name。

## 🏠 自定义登陆页面

可以自定义“网站”目录的内容以更改登录页面的外观。 大部分信息将自动填充来自 [`source.json`](source.json) 的信息。 不需要手动自定义登陆页面。

## 技术资料

欢迎您对自动化流程进行自己的更改，以使其满足您的需求，如果您认为我们应该采用一些更改，您可以创建拉取请求。 以下是有关所包含的自动化的更多信息：

### 构建列表
[build-listing.yml](.github/workflows/build-listing.yml)

这是一个复合操作，它根据您添加到 `source.json` 文件中的项目构建与 vpm 兼容的 [Repo 列表](https://vcc.docs.vrchat.com/vpm/repos)。 你已经创造了。 为了找到您的所有版本并将它们合并到一个列表中，它会检查[另一个存储库](https://github.com/vrchat-community/package-list-action)，其中有一个[Nuke](https:// /nuke.build/) 项目，其中包含 VPM 核心库以访问其类型和方法。 该项目将在未来扩展以包含更多功能 - 目前，该操作仅调用其“BuildRepoListing”目标，该目标在完成时调用“RebuildHomePage”。 如果您想要执行仅重建主页的操作，您可以直接调用它 - 只需复制现有调用并替换目标名称即可。
