iceboy5385@gmail.com---
ms.openlocfilehash: b15a09fa450995c55cc6e7313c51db4a3ba3f48a
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81316620"
---
# <a name="contributing"></a>参与

感谢你对贡献 Visual C++ 文档的关注！

本主题将介绍在 [Visual C++ 文档站点](https://docs.microsoft.com/cpp)中添加或更新内容的基本过程。

本主题将介绍：

- [参与流程](#process-for-contributing)
- [注意事项](#dos-and-donts)
- [生成文档](#building-the-docs)
- [提供示例](#contributing-to-samples)
- [贡献者许可协议](#contributor-license-agreement)

## <a name="process-for-contributing"></a>参与流程

**步骤 1：** 提出问题，描述你要编写的文章及其与现有内容的相关性。
“文档”文件夹中的内容按内容范围（例如，调试器）划分成不同的部分  。 为新内容确定正确的文件夹。 获取对建议的反馈。

可以稍作更改，跳过第一个步骤。

**步骤 2：** 创建`MicrosoftDocs/cpp-docs`存储库分支。

**步骤 3：** 为文章创建 `branch`。

**步骤 4：** 编写文章。

如果要新建主题，可以使用此[模板文件](./styleguide/template.md)作为起点。 它包含编写指南，还介绍了每篇文章所需的元数据，例如作者信息。

导航到与步骤 1 中为文章确定的 TOC 位置对应的文件夹。
该文件夹包含该部分中的所有文章的 Markdown 文件。 如有必要，可以创建一个新文件夹来放置内容文件。

对于图像和其他静态资源，请将其添加到名为 `media` 的子文件夹中。 如果要为内容创建新文件夹，请将媒体文件夹添加到新文件夹。

请务必遵循正确的 Markdown 语法。 有关详细信息，请参阅[风格指南](./styleguide/template.md)。

### <a name="example-structure"></a>结构示例

```
docs
    /standard-library
        wstring-convert-class.md
        /media
            wstring-conversion.png
```

**步骤 5：** 从分支中将拉取请求 (PR) 提交到 `MicrosoftDocs/cpp-docs/master`。

如果 PR 正在解决现有问题，请将 `Fixes #Issue_Number` 关键字添加到提交消息或 PR 描述中，以便在合并 PR 时自动关闭该问题。 有关详细信息，请参阅[通过提交消息关闭问题](https://help.github.com/articles/closing-issues-via-commit-messages/)。

Visual Studio 团队将审核 PR，并告知更改是否正常或是否需要进行任何其他更新/更改才能批准。

**步骤 6：** 与团队讨论后，对分支进行必要的更新。

一旦应用反馈且更改正常，维护人员会将 PR 合并到主分支。

我们会按一定的节奏，将所有提交的内容从主分支推送到实时分支，你将能在 [docs.microsoft.com](https://docs.microsoft.com/cpp/) 中实时看到你贡献的内容。

## <a name="dos-and-donts"></a>注意事项

下面是一个简短的指导规则列表，当你参与 .NET 文档时应牢记其中内容。

- 请勿发出大型拉取请求  。 可以提出问题并发起讨论，以便我们在你花费大量时间前确定方向。
- 请务必阅读[风格指南](./styleguide/template.md)以及[语气和语调](./styleguide/voice-tone.md)指南  。
- 请务必使用[模板](./styleguide/template.md)文件作为工作的起点  。
- 请务必在处理文章前，在分叉上创建一个单独的分支  。
- 请务必遵循 [GitHub 流工作流](https://guides.github.com/introduction/flow/)  。
- 请务必在博客和推文（或任何社交软件上）频繁地发布你的参与内容  ！

> [!NOTE]
> 你或许会注意到某些主题目前并没有遵循此处指定的所有准则和[风格指南](./styleguide/template.md)。 我们正努力实现整个站点的一致性。 请查看我们当前正在跟踪的有关此特定目标的[未解决问题](https://github.com/MicrosoftDocs/cpp-docs/issues?q=is%3Aissue+is%3Aopen+label%3Aguidelines-adherence)列表。

## <a name="building-the-docs"></a>生成文档

该文档使用[ GitHub Flavored Markdown ](https://help.github.com/categories/writing-on-github/)编写，并使用[ DocFX ](https://dotnet.github.io/docfx/)和其他内部发布/生成工具生成。 文档托管在 [docs.microsoft.com](https://docs.microsoft.com/)。

如果想要生成本地文档，则需要安装最新版的 [DocFX](https://dotnet.github.io/docfx/)。

有许多使用 DocFX 的方法，[DocFX 入门指南](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html)中介绍了其中的大多数方法。 以下说明使用该工具的[基于命令行的](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html#2-use-docfx-as-a-command-line-tool)版本。 如果你对以上链接中列出的其他方式更熟悉，可以使用这些方式。

**注意：** 当前的 DocFX 需要使用 .NET Framework（对于 Windows）或 Mono（对于 Linux 或 macOS）。 我们希望在将来将其移植到 .NET Core。

可以使用内置 Web 服务器在本地生成和预览生成的站点。 导航到计算机上的 `cpp-docs\docs` 文件夹并键入以下命令：

> docfx -t default --serve

这将在[ localhost：8080 ](http://localhost:8080)上启动本地预览。 然后可以通过转到 `http://localhost:8080/[path]`（如 `http://localhost:8080/cpp/visual-cpp-in-visual-studio.html`）查看所作的更改。

注意：本地预览目前不包含任何主题，因此外观和文档站点不同  。 我们正在努力改善体验。 我们还在嵌入式视频、备注和自带文档中使用了一些自定义扩展，预览版中不提供这些扩展。

## <a name="contributing-to-samples"></a>提供示例

现在，在文章中将所需示例代码作为内联代码块添加。 存储库中有一个 `codesnippets` 文件夹，但尚未准备好接受公众贡献的内容。

## <a name="contributor-license-agreement"></a>贡献者许可协议

在合并 PR 前，必须签署[贡献许可协议 (CLA)](LICENSE)。 对于 docs.microsoft.com 中项目的，只需签署一次即可。 可在维基百科上详细了解[贡献许可协议 (CLA)](https://en.wikipedia.org/wiki/Contributor_License_Agreement)。

无需事先签署该协议。 可如常克隆、创建分支并提交 PR。 创建 PR 后，将由 CLA 自动程序对其分类。 如果更改的内容十分琐碎（如修复了拼写错误），则 PR 会被标记为 CLA-not-required。 其他情况下，会分类为 CLA-required。 签署 CLA 后，当前和所有未来的拉取请求都会被标记为 CLA-signed。
