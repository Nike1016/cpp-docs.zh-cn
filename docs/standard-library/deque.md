---
title: '&lt;deque&gt;'
ms.date: 11/04/2016
f1_keywords:
- <deque>
helpviewer_keywords:
- deque header
ms.assetid: 4521fe92-5a91-4853-9e9f-59600bf9e46f
ms.openlocfilehash: a5fea8f4a1bc1612a35db71cc515ba4799e95da6
ms.sourcegitcommit: 590e488e51389066a4da4aa06d32d4c362c23393
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2019
ms.locfileid: "72689730"
---
# <a name="ltdequegt"></a>&lt;deque&gt;

定义容器类模板 deque 和多个支持模板。

## <a name="requirements"></a>要求

**标头**：\<deque>

> [!NOTE]
> > 库 \<deque 也使用了 `#include <initializer_list>` 语句。

## <a name="members"></a>Members

### <a name="operators"></a>运算符

|||
|-|-|
|[operator!=](../standard-library/deque-operators.md#op_neq)|测试运算符左侧的 deque 对象是否不等于右侧的 deque 对象。|
|[operator<](../standard-library/deque-operators.md#op_lt)|测试运算符左侧的 deque 对象是否小于右侧的 deque 对象。|
|[operator\<=](../standard-library/deque-operators.md#op_gt_eq)|测试运算符左侧的 deque 对象是否小于或等于右侧的 deque 对象。|
|[operator==](../standard-library/deque-operators.md#op_eq_eq)|测试运算符左侧的 deque 对象是否等于右侧的 deque 对象。|
|[operator>](../standard-library/deque-operators.md#op_gt)|测试运算符左侧的 deque 对象是否大于右侧的 deque 对象。|
|[operator>=](../standard-library/deque-operators.md#op_gt_eq)|测试运算符左侧的 deque 对象是否大于或等于右侧的 deque 对象。|

### <a name="functions"></a>函数

|||
|-|-|
|[swap](../standard-library/deque-functions.md#swap)|交换两个 deque 的元素。|

### <a name="classes"></a>类

|||
|-|-|
|[deque 类](../standard-library/deque-class.md)|序列容器的类模板，用于排列线性排列中给定类型的元素，例如向量，允许快速随机访问任何元素和在容器后面高效插入和删除。|

## <a name="see-also"></a>请参阅

[头文件引用](../standard-library/cpp-standard-library-header-files.md)\
[C++ 标准库中的线程安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[C++ 标准库参考](../standard-library/cpp-standard-library-reference.md)
