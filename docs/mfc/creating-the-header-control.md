---
title: 创建标题控件
ms.date: 11/04/2016
helpviewer_keywords:
- CHeaderCtrl class [MFC], creating
- header controls [MFC], creating
ms.assetid: 7864d9d2-4a2c-4622-b58b-7b110a1e28d2
ms.openlocfilehash: b08dd4d3f12c70ae495b20b936d44f6a695d1ae1
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84616246"
---
# <a name="creating-the-header-control"></a>创建标题控件

标头控件不能直接在对话框编辑器中使用（尽管可以添加包含标题控件的列表控件）。

### <a name="to-put-a-header-control-in-a-dialog-box"></a>在对话框中放置标头控件

1. 在对话框类中手动嵌入类型为[CHeaderCtrl](reference/cheaderctrl-class.md)的成员变量。

1. 在[OnInitDialog](reference/cdialog-class.md#oninitdialog)中，创建并设置的样式 `CHeaderCtrl` ，定位它并显示它。

1. 向标题控件添加项。

1. 使用[类向导](reference/mfc-class-wizard.md)可以在对话框类中映射您需要处理的任何标头控件通知消息（请参阅[将消息映射到函数](reference/mapping-messages-to-functions.md)）。

### <a name="to-put-a-header-control-in-a-view-not-a-clistview"></a>将标头控件置于视图中（不是 CListView）

1. 在视图类中嵌入一个[CHeaderCtrl](reference/cheaderctrl-class.md)对象。

1. 样式、位置，并显示视图的[OnInitialUpdate](reference/cview-class.md#oninitialupdate)成员函数中的标题控件窗口。

1. 向标题控件添加项。

1. 使用[类向导](reference/mfc-class-wizard.md)可以在视图类中映射您需要处理的任何标头控件通知消息（请参阅[将消息映射到函数](reference/mapping-messages-to-functions.md)）。

在任一情况下，都将在创建视图或对话框对象时创建嵌入控件对象。 然后，必须调用[CHeaderCtrl：： create](reference/cheaderctrl-class.md#create)来创建控件窗口。 若要确定控件的位置，可调用[CHeaderCtrl：： Layout](reference/cheaderctrl-class.md#layout)来确定控件的初始大小和位置，并将[SetWindowPos](reference/cwnd-class.md#setwindowpos)设置为所需的位置。 然后按向[标题控件添加项](adding-items-to-the-header-control.md)中所述添加项。

有关详细信息，请参阅在 Windows SDK 中[创建标题控件](/windows/win32/Controls/header-controls)。

## <a name="see-also"></a>另请参阅

[使用 CHeaderCtrl](using-cheaderctrl.md)<br/>
[控件](controls-mfc.md)
