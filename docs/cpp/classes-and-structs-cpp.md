---
title: 类和结构 (C++)
ms.date: 05/07/2019
helpviewer_keywords:
- C++, classes and structs
ms.assetid: 516dd496-13fb-4f17-845a-e9ca45437873
ms.openlocfilehash: 19d95c9519670db39f3ca467aff794233823d7ba
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2020
ms.locfileid: "80180883"
---
# <a name="classes-and-structs-c"></a>类和结构 (C++)

此部分介绍 C++ 类和结构。 这两个构造在 C++ 中是相同的，只不过在结构中，默认可访问性是公共的，而在类中，默认值是私有的。

类和结构是用于定义你自己的类型的构造。 类和结构都可以包含数据成员和成员函数，使你可以描述类型的状态和行为。

包含以下主题：

- [class](../cpp/class-cpp.md)

- [struct](../cpp/struct-cpp.md)

- [类成员概述](../cpp/class-member-overview.md)

- [成员访问控制](../cpp/member-access-control-cpp.md)

- [继承](../cpp/inheritance-cpp.md)

- [静态成员](../cpp/static-members-cpp.md)

- [用户定义的类型转换](../cpp/user-defined-type-conversions-cpp.md)

- [可变数据成员（可变说明符）](../cpp/mutable-data-members-cpp.md)

- [嵌套类声明](../cpp/nested-class-declarations.md)

- [匿名类类型](../cpp/anonymous-class-types.md)

- [指向成员的指针](../cpp/pointers-to-members.md)

- [this 指针](../cpp/this-pointer.md)

- [C++ 位域](../cpp/cpp-bit-fields.md)

三种类类型是结构、类和联合。 它们使用[结构](../cpp/struct-cpp.md)、[类](../cpp/class-cpp.md)和[联合](../cpp/unions.md)关键字进行声明。 下表显示三种类类型之间的差异。

有关联合的详细信息，请参阅[联合](../cpp/unions.md)。 有关/Cli 和C++ C++/cx 中的类和结构的信息，请参阅[类和结构](../extensions/classes-and-structs-cpp-component-extensions.md)。

### <a name="access-control-and-constraints-of-structures-classes-and-unions"></a>结构、类和联合的访问控制和约束

|结构|类|Unions|
|----------------|-------------|------------|
|类键是**结构**|类键是**类**|类键是**union**|
|默认访问是公共的|默认访问是私有的|默认访问是公共的|
|没有使用约束|没有使用约束|一次只使用一个成员|

## <a name="see-also"></a>请参阅

[C++ 语言参考](../cpp/cpp-language-reference.md)
