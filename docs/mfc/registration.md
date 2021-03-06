---
title: 注册
ms.date: 11/04/2016
helpviewer_keywords:
- servers [MFC], initializing
- initializing servers [MFC]
- OLE, registration
- installing servers [MFC]
- registry [MFC], OLE item database
- registration databases [MFC]
- servers [MFC], installing
- OLE server applications [MFC], registering servers
ms.assetid: 991d5684-72c1-4f9e-a09a-9184ed12bbb9
ms.openlocfilehash: 82411e53620e92eff3484f7d3f7955030fd439ac
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81372843"
---
# <a name="registration"></a>注册

当用户需要将一个 OLE 项插入应用程序中时，OLE 会显示一个对象类型的列表以供选择。 OLE 从系统注册数据库获取此列表，该数据库包含所有服务器应用程序提供的信息。 当服务器注册自身时，它放入系统注册数据库（注册表）中的项将描述它提供的每种对象类型、文件扩展名、自身的路径以及其他信息。

框架和 OLE 系统动态链接库 (DLL) 使用此注册表确定系统上提供了哪些类型的 OLE 项。 OLE 系统 DLL 还使用此注册表确定在激活链接的或嵌入的对象时如何启动服务器应用程序。

本文介绍了在安装和每次执行服务器应用程序时，该应用程序需要执行的操作。

有关系统注册数据库和用于更新它的 .reg 文件的格式的详细信息，请参阅*OLE 程序员的参考*。

## <a name="server-installation"></a><a name="_core_server_installation"></a>服务器安装

在首次安装服务器应用程序时，应注册它所支持的所有类型的 OLE 项。 您也可以让服务器在每次将系统注册数据库作为独立的应用程序执行时对其进行更新。 这可在移动服务器的可执行文件时保持注册数据库最新。

> [!NOTE]
> 由应用程序向导生成的 MFC 应用程序在作为独立的应用程序运行时将自动注册自身。

如果您需要在安装期间注册应用程序，请使用 RegEdit.exe 程序。 如果包含应用程序的安装程序，请让安装程序运行"RegEdit /S*应用程序名称*.reg"。 （/S 标志指示静默操作，即它不显示报告成功完成命令的对话框。否则，请指示用户手动运行 RegEdit。

> [!NOTE]
> 由应用程序向导创建的 .reg 文件不包含可执行文件的完整路径。 安装程序必须修改 .reg 文件来包含可执行文件的完整路径，或修改 PATH 环境变量来包含安装目录。

RegEdit 将 .reg 文本文件的内容合并到注册数据库中。 若要验证数据库或修复它，请使用注册表编辑器。 注意避免删除必需的 OLE 项。

## <a name="server-initialization"></a><a name="_core_server_initialization"></a>服务器初始化

在使用应用程序向导创建服务器应用程序时，该向导将自动为你完成所有初始化任务。 本节介绍了在手动编写服务器应用程序时您必须执行的操作。

当服务器应用程序由容器应用程序启动时，OLE 系统 DLL 会将“/Embedding”选项添加到服务器的命令行中。 服务器应用程序的行为因其是否由容器启动而异，因此应用程序在开始执行时应执行的第一个操作是检查命令行上的“/Embedding”或“-Embedding”选项。 如果此开关存在，则加载一组不同的资源，这些资源显示服务器处于就地活动状态或完全打开状态。 有关详细信息，请参阅[菜单和资源：服务器添加](../mfc/menus-and-resources-server-additions.md)。

服务器应用程序还应调用其 `CWinApp::RunEmbedded` 函数来分析命令行。 如果返回非零值，则应用程序将不会显示其窗口，因为它已从容器应用程序运行，而不是作为独立的应用程序运行。 此函数会在系统注册数据库中更新服务器的条目，并调用 `RegisterAll` 成员函数，还将执行实例注册。

当服务器应用程序启动时，您必须确保它可以执行实例注册。 实例注册告知 OLE 系统 DLL 此服务器处于活动状态并准备接收来自容器的请求。 它不会将条目添加到注册数据库中。 通过调用由 `ConnectTemplate` 定义的 `COleTemplateServer` 成员函数来执行服务器的实例注册。 这会将 `CDocTemplate` 对象连接到 `COleTemplateServer` 对象。

该`ConnectTemplate`函数采用三个参数：服务器的*CLSID、* 指向`CDocTemplate`对象的指针和指示服务器是否支持多个实例的标志。 miniserver 必须能够支持多个实例，也就是说，多个服务器实例必须能够同时运行，一个实例对应一个容器。 因此，在启动迷你服务器时，将此标志传递**TRUE。**

如果您编写 miniserver，根据定义，它将始终由容器启动。 您仍应分析命令行以检查“/Embedding”选项。 命令行上缺少此选项意味着用户已尝试将 miniserver 作为独立的应用程序启动。 如果发生这种情况，请向系统注册数据库注册此服务器，然后显示一个消息框，通知用户从容器应用程序启动 miniserver。

## <a name="see-also"></a>另请参阅

[OLE](../mfc/ole-in-mfc.md)<br/>
[服务器](../mfc/servers.md)<br/>
[CWinApp：：运行自动](../mfc/reference/cwinapp-class.md#runautomated)<br/>
[CWinApp：：运行嵌入式](../mfc/reference/cwinapp-class.md#runembedded)<br/>
[COleTemplateServer 类](../mfc/reference/coletemplateserver-class.md)
