---
title: TZNAME_MAX
ms.date: 10/22/2018
f1_keywords:
- TZNAME_MAX
helpviewer_keywords:
- TZNAME_MAX constant
ms.assetid: e2286cb8-751d-4557-9650-5c4b98a8f7be
ms.openlocfilehash: 71e5becd39f49d86573483c5451a9a2415d84181
ms.sourcegitcommit: dedd4c3cb28adec3793329018b9163ffddf890a4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/11/2019
ms.locfileid: "57750931"
---
# <a name="tznamemax"></a>TZNAME_MAX

**已过时**。 时区名称变量允许的最大字符串长度。 Visual Studio 2012 和早期版本中的 \<limits.h> 定义了此宏。 Visual Studio 2013 及更高版本中未定义它。 要获取保存当前时区名称所需的长度，请使用 [_get_tzname](../c-runtime-library/reference/get-tzname.md)。

## <a name="syntax"></a>语法

```
#include <limits.h>
```

## <a name="see-also"></a>请参阅

[环境常量](../c-runtime-library/environmental-constants.md)<br/>
[全局常量](../c-runtime-library/global-constants.md)<br/>
[_get_tzname](../c-runtime-library/reference/get-tzname.md)
