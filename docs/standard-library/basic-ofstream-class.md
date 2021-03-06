---
title: basic_ofstream 类
ms.date: 11/04/2016
f1_keywords:
- fstream/std::basic_ofstream
- fstream/std::basic_ofstream::close
- fstream/std::basic_ofstream::is_open
- fstream/std::basic_ofstream::open
- fstream/std::basic_ofstream::rdbuf
- fstream/std::basic_ofstream::swap
helpviewer_keywords:
- std::basic_ofstream [C++]
- std::basic_ofstream [C++], close
- std::basic_ofstream [C++], is_open
- std::basic_ofstream [C++], open
- std::basic_ofstream [C++], rdbuf
- std::basic_ofstream [C++], swap
ms.assetid: 3bcc9c51-6dfc-4844-8fcc-22ef57c9dff1
ms.openlocfilehash: f2d0facd92e0ef1935f8218a6d323a62edb81e5b
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81376785"
---
# <a name="basic_ofstream-class"></a>basic_ofstream 类

描述一个对象，它控制将元素和编码的对象插入类[basic_filebuf](../standard-library/basic-filebuf-class.md)< `Elem`的流缓冲区中，>，`Tr`其元素的类型`Elem`由类`Tr`确定。

## <a name="syntax"></a>语法

```cpp
template <class Elem, class Tr = char_traits<Elem>>
class basic_ofstream : public basic_ostream<Elem, Tr>
```

### <a name="parameters"></a>参数

*埃莱姆*\
文件缓冲区的基本元素。

*Tr*\
文件缓冲区的基本元素的特征（通常是 `char_traits`< `Elem`>）。

## <a name="remarks"></a>备注

当**wchar_t**写入文件的专门`basic_ofstream`化时，如果文件以文本模式打开，它将写入 MBCS 序列。 内部表示形式将使用 `wchar_t` 字符的缓冲区。

该对象存储 `basic_filebuf`< `Elem`, `Tr`> 类的对象。

## <a name="example"></a>示例

下面的示例演示了如何创建 `basic_ofstream` 对象和向其写入文本。

```cpp
// basic_ofstream_class.cpp
// compile with: /EHsc
#include <fstream>

using namespace std;

int main(int argc, char **argv)
{
    ofstream ofs("ofstream.txt");
    if (!ofs.bad())
    {
        ofs << "Writing to a basic_ofstream object..." << endl;
        ofs.close();
    }
}
```

### <a name="constructors"></a>构造函数

|构造函数|说明|
|-|-|
|[basic_ofstream](#basic_ofstream)|创建一个 `basic_ofstream` 类型的对象。|

### <a name="member-functions"></a>成员职能

|成员函数|说明|
|-|-|
|[关闭](#close)|关闭文件。|
|[is_open](#is_open)|确定文件是否打开。|
|[open](#open)|打开文件。|
|[rdbuf](#rdbuf)|返回存储的流缓冲区的地址。|
|[交换](#swap)|将此 `basic_ofstream` 的内容与提供的 `basic_ofstream` 的内容进行交换。|

### <a name="operators"></a>运算符

|操作员|说明|
|-|-|
|[运算符*](#op_eq)|分配此流对象的内容。 这是一种移动赋值，所涉及的 `rvalue reference` 不会留下副本。|

## <a name="requirements"></a>要求

**标头：** \<fstream>

**命名空间:** std

## <a name="basic_ofstreambasic_ofstream"></a><a name="basic_ofstream"></a>basic_ofstream：basic_ofstream

创建一个 `basic_ofstream` 类型的对象。

```cpp
basic_ofstream();

explicit basic_ofstream(
    const char* _Filename,
    ios_base::openmode _Mode = ios_base::out,
    int _Prot = (int)ios_base::_Openprot);

explicit basic_ofstream(
    const wchar_t* _Filename,
    ios_base::openmode _Mode = ios_base::out,
    int _Prot = (int)ios_base::_Openprot);

basic_ofstream(
    basic_ofstream&& right);
```

### <a name="parameters"></a>参数

*_Filename*\
要打开的文件的名称。

*_Mode*\
[ios_base::openmode](../standard-library/ios-base-class.md#openmode) 中的枚举之一。

*_Prot*\
默认文件打开保护，等同于 [_fsopen、_wfsopen](../c-runtime-library/reference/fsopen-wfsopen.md) 中的 `shflag` 参数。

*对*\
对 `basic_ofstream` 对象的右值引用用于初始化此 `basic_ofstream` 对象。

### <a name="remarks"></a>备注

第一个构造函数通过调用[basic_ostream](../standard-library/basic-ostream-class.md)`sb`（） 来初始化基`sb`类，其中类[basic_filebuf](../standard-library/basic-filebuf-class.md)< `Elem`的存储对象`Tr`>。 通过调用 `basic_filebuf`< `Elem`, `Tr`>，它还可以初始化 `sb`。

通过调用 `basic_ostream`( **sb**)，第二个和第三个构造函数可初始化基类。 `sb`它还通过`basic_filebuf`< `Elem`调用`Tr`、>然后`sb`初始化。 [打开](../standard-library/basic-filebuf-class.md#open) `_Filename`（， `ios_base::out`&#124; `_Mode` ）。 如果后一个函数返回空指针，则构造函数将调用[setstate](../standard-library/basic-ios-class.md#setstate)（`failbit`。

第四个构造函数是一个 copy 函数。 它用*右侧*的内容初始化对象，作为 rvalue 引用。

### <a name="example"></a>示例

下面的示例演示了如何创建 `basic_ofstream` 对象和向其写入文本。

```cpp
// basic_ofstream_ctor.cpp
// compile with: /EHsc
#include <fstream>

using namespace std;

int main(int argc, char **argv)
{
    ofstream ofs("C:\\ofstream.txt");
    if (!ofs.bad())
    {
        ofs << "Writing to a basic_ofstream object..." << endl;
        ofs.close();
    }
}
```

## <a name="basic_ofstreamclose"></a><a name="close"></a>basic_ofstream：关闭

关闭文件。

```cpp
void close();
```

### <a name="remarks"></a>备注

成员函数调用[rdbuf](../standard-library/basic-ifstream-class.md#rdbuf)**->**[关闭](../standard-library/basic-filebuf-class.md#close)。

### <a name="example"></a>示例

有关如何使用 `close` 的示例，请参阅 [basic_filebuf::close](../standard-library/basic-filebuf-class.md#close)。

## <a name="basic_ofstreamis_open"></a><a name="is_open"></a>basic_ofstream：is_open

指示文件是否打开。

```cpp
bool is_open() const;
```

### <a name="return-value"></a>返回值

如果文件处于打开状态，则为 **true**，否则为 **false**。

### <a name="remarks"></a>备注

成员函数返回[rdbuf](#rdbuf) **->** [is_open](../standard-library/basic-filebuf-class.md#is_open)。

### <a name="example"></a>示例

```cpp
// basic_ofstream_is_open.cpp
// compile with: /EHsc
#include <fstream>
#include <iostream>

int main( )
{
   using namespace std;
   ifstream file;
   // Open and close with a basic_filebuf
   file.rdbuf( )->open( "basic_ofstream_is_open.txt", ios::in );
   file.close( );
   if (file.is_open())
      cout << "it's open" << endl;
   else
      cout << "it's closed" << endl;
}
```

## <a name="basic_ofstreamopen"></a><a name="open"></a>basic_ofstream：：打开

打开文件。

```cpp
void open(
    const char* _Filename,
    ios_base::openmode _Mode = ios_base::out,
    int _Prot = (int)ios_base::_Openprot);

void open(
    const char* _Filename,
    ios_base::openmode _Mode);

void open(
    const wchar_t* _Filename,
    ios_base::openmode _Mode = ios_base::out,
    int _Prot = (int)ios_base::_Openprot);

void open(
    const wchar_t* _Filename,
    ios_base::openmode _Mode);
```

### <a name="parameters"></a>参数

*_Filename*\
要打开的文件的名称。

*_Mode*\
[ios_base::openmode](../standard-library/ios-base-class.md#openmode) 中的枚举之一。

*_Prot*\
默认文件打开保护，等同于 [_fsopen、_wfsopen](../c-runtime-library/reference/fsopen-wfsopen.md) 中的 `shflag` 参数。

### <a name="remarks"></a>备注

成员函数调用[rdbuf](#rdbuf) **->** [打开](../standard-library/basic-filebuf-class.md#open)（*`_Mode`*文件名*，&#124; `ios_base::out`）。 如果该函数返回空指针，则函数将调用[setstate](../standard-library/basic-ios-class.md#setstate)（`failbit`。

### <a name="example"></a>示例

有关使用`open`的示例，请参阅[basic_filebuf：：打开](../standard-library/basic-filebuf-class.md#open)。

## <a name="basic_ofstreamoperator"></a><a name="op_eq"></a>basic_ofstream：：操作员*

分配此流对象的内容。 这是一种移动赋值，所涉及的 `rvalue reference` 不会留下副本。

```cpp
basic_ofstream& operator=(basic_ofstream&& right);
```

### <a name="parameters"></a>参数

*对*\
对 `basic_ofstream` 对象的右值引用。

### <a name="return-value"></a>返回值

返回 `*this`。

### <a name="remarks"></a>备注

成员运算符使用*权利*的内容替换对象的内容，该内容被视为 rvalue 引用。

## <a name="basic_ofstreamrdbuf"></a><a name="rdbuf"></a>basic_ofstream：：rdbuf

返回存储的流缓冲区的地址。

```cpp
basic_filebuf<Elem, Tr> *rdbuf() const
```

### <a name="return-value"></a>返回值

返回存储的流缓冲区的地址。

### <a name="example"></a>示例

有关如何使用 `rdbuf` 的示例，请参阅 [basic_filebuf::close](../standard-library/basic-filebuf-class.md#close)。

## <a name="basic_ofstreamswap"></a><a name="swap"></a>basic_ofstream：交换

交换两个 `basic_ofstream` 对象的内容。

```cpp
void swap(basic_ofstream& right);
```

### <a name="parameters"></a>参数

*对*\
对另一个 `basic_ofstream` 对象的 `lvalue` 引用。

### <a name="remarks"></a>备注

成员函数将此对象的内容交换为*权利*的内容。

## <a name="see-also"></a>另请参阅

[basic_ostream类](../standard-library/basic-ostream-class.md)\
[C++标准库中的线程安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[电流编程](../standard-library/iostream-programming.md)\
[iostreams 约定](../standard-library/iostreams-conventions.md)
