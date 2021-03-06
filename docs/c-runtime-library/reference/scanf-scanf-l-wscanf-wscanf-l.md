﻿---
title: scanf、_scanf_l、wscanf、_wscanf_l
ms.date: 10/21/2019
api_name:
- _wscanf_l
- scanf
- _scanf_l
- wscanf
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
- _tscanf
- _scanf_l
- wscanf
- _wscanf_l
- scanf
- _tscanf_l
helpviewer_keywords:
- tscanf_l function
- _tscanf_l function
- reading data [C++], from input streams
- _tscanf function
- data [C++], reading from input stream
- scanf_l function
- scanf function
- wscanf function
- _scanf_l function
- tscanf function
- formatted data [C++], from input streams
- wscanf_l function
- _wscanf_l function
ms.assetid: 73eac607-117f-4be4-9ff0-4afd9cf3c848
ms.openlocfilehash: df63baa8ffa878a4a65c84e07f0e68aa383e79cf
ms.sourcegitcommit: 8e285a766523e653aeeb34d412dc6f615ef7b17b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "80079213"
---
# <a name="scanf-_scanf_l-wscanf-_wscanf_l"></a>scanf、_scanf_l、wscanf、_wscanf_l

读取标准输入流中的格式化数据。 提供这些函数的更多安全版本；请参阅 [scanf_s、_scanf_s_l、wscanf_s、_wscanf_s_l](scanf-s-scanf-s-l-wscanf-s-wscanf-s-l.md)。

> [!NOTE]
> 在 Visual Studio 2015 中，`printf` 和 `scanf` 系列函数被声明为**内联**，并移到 `<stdio.h>` 和 `<conio.h>` 标头。 如果迁移的是较旧的代码，则与这些函数的连接可能会出现*LNK2019* 。 有关详细信息，请[参阅C++ Visual change history 2003-2015](../../porting/visual-cpp-change-history-2003-2015.md#stdio_and_conio)。

## <a name="syntax"></a>语法

```C
int scanf(
   const char *format [,
   argument]...
);
int _scanf_l(
   const char *format,
   locale_t locale [,
   argument]...
);
int wscanf(
   const wchar_t *format [,
   argument]...
);
int _wscanf_l(
   const wchar_t *format,
   locale_t locale [,
   argument]...
);
```

### <a name="parameters"></a>parameters

format<br/>
格式控制字符串。

argument<br/>
可选参数。

*locale*<br/>
要使用的区域设置。

## <a name="return-value"></a>返回值

返回已成功转换和分配的字段数量；返回值不包括已读取但未分配的字段。 返回值为 0 表示没有分配任何字段。

如果*format*为**空**指针，则将调用无效参数处理程序，如[参数验证](../../c-runtime-library/parameter-validation.md)中所述。 如果允许执行继续，则这些函数将返回**EOF** ，并将**Errno**设置为**EINVAL**。

有关这些代码及其他错误代码的信息，请参阅 [_doserrno、errno、_sys_errlist 和 _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)。

## <a name="remarks"></a>备注

**Scanf**函数从标准输入流**stdin**中读取数据，并将数据写入到由*参数*给定的位置。 每个*参数*都必须是指向类型的变量的指针，该类型与*格式*中的类型说明符对应。 如果复制出现在重叠的字符串之间，则该行为不确定。

> [!IMPORTANT]
> 使用**scanf**读取字符串时，请始终指定 **% s**格式的宽度（例如， **"% 32s"** 而不是 **"% s"** ）;否则，输入格式不正确可能会导致缓冲区溢出。 或者，可以考虑使用 [scanf_s、_scanf_s_l、wscanf_s、_wscanf_s_l](scanf-s-scanf-s-l-wscanf-s-wscanf-s-l.md) 或 [fgets](fgets-fgetws.md)。

**wscanf**是**scanf**的宽字符版本;**wscanf**的*格式*参数是宽字符字符串。 如果在 ANSI 模式下打开流，则**wscanf**和**scanf**的行为相同。 **scanf**当前不支持 UNICODE 流的输入。

这些具有 **_l**后缀的函数的版本相同，只不过它们使用传入的区域设置参数而不是当前线程区域设置。

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|TCHAR.H 例程|未定义 _UNICODE 和 _MBCS|已定义 _MBCS|已定义 _UNICODE|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_tscanf**|**scanf**|**scanf**|**wscanf**|
|**_tscanf_l**|**_scanf_l**|**_scanf_l**|**_wscanf_l**|

有关详细信息，请参阅[格式规范字段 — scanf 函数和 wscanf 函数](../../c-runtime-library/format-specification-fields-scanf-and-wscanf-functions.md)。

## <a name="requirements"></a>要求

|例程|必需的标头|
|-------------|---------------------|
|**scanf**、 **_scanf_l**|\<stdio.h>|
|**wscanf**、 **_wscanf_l**|\<stdio.h> 或 \<wchar.h>|

通用 Windows 平台（UWP）应用中不支持控制台。 与控制台、 **stdin**、 **stdout**和**stderr**关联的标准流句柄必须重定向，然后 C 运行时函数才能在 UWP 应用中使用它们。 有关其他兼容性信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

```C
// crt_scanf.c
// compile with: /W3
// This program uses the scanf and wscanf functions
// to read formatted input.

#include <stdio.h>

int main( void )
{
   int   i, result;
   float fp;
   char  c, s[81];
   wchar_t wc, ws[81];
   result = scanf( "%d %f %c %C %80s %80S", &i, &fp, &c, &wc, s, ws ); // C4996
   // Note: scanf and wscanf are deprecated; consider using scanf_s and wscanf_s
   printf( "The number of fields input is %d\n", result );
   printf( "The contents are: %d %f %c %C %s %S\n", i, fp, c, wc, s, ws);
   result = wscanf( L"%d %f %hc %lc %80S %80ls", &i, &fp, &c, &wc, s, ws ); // C4996
   wprintf( L"The number of fields input is %d\n", result );
   wprintf( L"The contents are: %d %f %C %c %hs %s\n", i, fp, c, wc, s, ws);
}
```

```Input
71 98.6 h z Byte characters
36 92.3 y n Wide characters
```

```Output
The number of fields input is 6
The contents are: 71 98.599998 h z Byte characters
The number of fields input is 6
The contents are: 36 92.300003 y n Wide characters
```

## <a name="see-also"></a>另请参阅

[浮点支持](../../c-runtime-library/floating-point-support.md)<br/>
[流 I/O](../../c-runtime-library/stream-i-o.md)<br/>
[区域设置](../../c-runtime-library/locale.md)<br/>
[fscanf、_fscanf_l、fwscanf、_fwscanf_l](fscanf-fscanf-l-fwscanf-fwscanf-l.md)<br/>
[printf、_printf_l、wprintf、_wprintf_l](printf-printf-l-wprintf-wprintf-l.md)<br/>
[sprintf、_sprintf_l、swprintf、_swprintf_l、\__swprintf_l](sprintf-sprintf-l-swprintf-swprintf-l-swprintf-l.md)<br/>
[sscanf、_sscanf_l、swscanf、_swscanf_l](sscanf-sscanf-l-swscanf-swscanf-l.md)<br/>
