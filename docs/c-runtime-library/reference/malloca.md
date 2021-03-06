---
title: _malloca
ms.date: 11/04/2016
api_name:
- _malloca
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- malloca
- _malloca
helpviewer_keywords:
- memory allocation, stack
- malloca function
- _malloca function
ms.assetid: 293992df-cfca-4bc9-b313-0a733a6bb936
ms.openlocfilehash: 0b12b4adde710f2fc46b3a3790519006fabbb1fc
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2019
ms.locfileid: "70952774"
---
# <a name="_malloca"></a>_malloca

在堆栈上分配内存。 这是 [_alloca](alloca.md) 版本，具有 [CRT 中的安全功能](../../c-runtime-library/security-features-in-the-crt.md)中所述的安全增强功能。

## <a name="syntax"></a>语法

```C
void *_malloca(
   size_t size
);
```

### <a name="parameters"></a>参数

*size*<br/>
在堆栈中要分配的字节数。

## <a name="return-value"></a>返回值

**_Malloca**例程返回指向已分配空间的**void**指针，该指针保证能针对任何类型的对象的存储进行适当的调整。 如果*size*为0，则 **_malloca**将分配一个长度为零的项，并返回指向该项的有效指针。

如果*size*大于 **_ALLOCA_S_THRESHOLD**，则 **_malloca**将尝试在堆上分配，如果无法分配空间，则返回空指针。 如果*size*小于或等于 **_ALLOCA_S_THRESHOLD**，则 **_malloca**尝试在堆栈上分配，并在无法分配空间时生成堆栈溢出异常。 堆栈溢出异常不是C++异常;这是结构化异常。 您必须使用C++ [结构化异常处理](../../cpp/structured-exception-handling-c-cpp.md)（SEH）来捕获此异常，而不是使用异常处理。

## <a name="remarks"></a>备注

如果请求超出了 **_ALLOCA_S_THRESHOLD**给定的特定大小（以字节为单位）， **_malloca**将从程序堆栈或堆分配*大小*字节。 **_Malloca**和 **_alloca**之间的差异在于，无论大小如何， **_alloca**始终在堆栈上分配。 与 **_alloca**不同，不要求或不允许调用**自由**释放内存以便分配， **_malloca**需要使用[_freea](freea.md)来释放内存。 在调试模式下， **_malloca**始终从堆中分配内存。

在异常处理程序（EH）中显式调用 **_malloca**存在一些限制。 在 x86 类处理器上运行的 EH 例程在其自己的内存帧中运行：它们在内存空间中执行其任务，这些任务不基于封闭函数的堆栈指针的当前位置。 最常见的实现包括 Windows NT 结构化异常处理 (SEH) 和 C++ catch 子句表达式。 因此，在以下任何一种情况下，显式调用 **_malloca**会导致在返回到调用 EH 例程期间程序失败：

- Windows NT SEH 异常筛选器表达式 ： __except`_malloca ()` （）

- Windows NT SEH 最终异常处理程序 ： __finally`_malloca ()` {}

- C++ EH catch 子句表达式

但是，可以从 EH 例程内或从应用程序提供的回调中直接调用 **_malloca** ，该回调由前面列出的某个 EH 方案调用。

> [!IMPORTANT]
> 在 Windows XP 中，如果在 try/catch 块中调用 **_malloca** ，则必须在 catch 块中调用[_resetstkoflw](resetstkoflw.md) 。

除了上述限制之外，在使用[/clr （公共语言运行时编译）](../../build/reference/clr-common-language-runtime-compilation.md)选项时， **_malloca**不能在 **__except**块中使用。 有关详细信息，请参阅 [/clr Restrictions](../../build/reference/clr-restrictions.md)。

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**_malloca**|\<malloc.h>|

## <a name="example"></a>示例

```C
// crt_malloca_simple.c
#include <stdio.h>
#include <malloc.h>

void Fn()
{
   char * buf = (char *)_malloca( 100 );
   // do something with buf
   _freea( buf );
}

int main()
{
   Fn();
}
```

## <a name="example"></a>示例

```C
// crt_malloca_exception.c
// This program demonstrates the use of
// _malloca and trapping any exceptions
// that may occur.

#include <windows.h>
#include <stdio.h>
#include <malloc.h>

int main()
{
    int     size;
    int     numberRead = 0;
    int     errcode = 0;
    void    *p = NULL;
    void    *pMarker = NULL;

    while (numberRead == 0)
    {
        printf_s("Enter the number of bytes to allocate "
                 "using _malloca: ");
        numberRead = scanf_s("%d", &size);
    }

    // Do not use try/catch for _malloca,
    // use __try/__except, since _malloca throws
    // Structured Exceptions, not C++ exceptions.

    __try
    {
        if (size > 0)
        {
            p =  _malloca( size );
        }
        else
        {
            printf_s("Size must be a positive number.");
        }
        _freea( p );
    }

    // Catch any exceptions that may occur.
    __except( GetExceptionCode() == STATUS_STACK_OVERFLOW )
    {
        printf_s("_malloca failed!\n");

        // If the stack overflows, use this function to restore.
        errcode = _resetstkoflw();
        if (errcode)
        {
            printf("Could not reset the stack!");
            _exit(1);
        }
    };
}
```

### <a name="input"></a>输入

```Input
1000
```

### <a name="sample-output"></a>示例输出

```Output
Enter the number of bytes to allocate using _malloca: 1000
```

## <a name="see-also"></a>请参阅

[内存分配](../../c-runtime-library/memory-allocation.md)<br/>
[calloc](calloc.md)<br/>
[malloc](malloc.md)<br/>
[realloc](realloc.md)<br/>
[_resetstkoflw](resetstkoflw.md)<br/>
