---
title: 型のマーシャリング - .NET
description: .NET が型をネイティブ表現にマーシャリングする方法について説明します。
author: jkoritzinsky
ms.author: jekoritz
ms.date: 01/18/2019
ms.openlocfilehash: 2c62581d34e77f208b7764f955dfa37613615ee4
ms.sourcegitcommit: b56d59ad42140d277f2acbd003b74d655fdbc9f1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/19/2019
ms.locfileid: "56411429"
---
# <a name="type-marshalling"></a><span data-ttu-id="d82cf-103">型のマーシャリング</span><span class="sxs-lookup"><span data-stu-id="d82cf-103">Type marshalling</span></span>

<span data-ttu-id="d82cf-104">**マーシャリング**とは、マネージド コードとネイティブ コードの間でやり取りする必要がある場合に型を変換するプロセスです。</span><span class="sxs-lookup"><span data-stu-id="d82cf-104">**Marshalling** is the process of transforming types when they need to cross between managed and native code.</span></span>

<span data-ttu-id="d82cf-105">マネージド コードとアンマネージド コード内の型は異なるため、マーシャリングが必要です。</span><span class="sxs-lookup"><span data-stu-id="d82cf-105">Marshalling is needed because the types in the managed and unmanaged code are different.</span></span> <span data-ttu-id="d82cf-106">マネージド コードで、たとえば、`String` があるとします。アンマネージド環境では、文字列は Unicode ("ワイド")、Unicode 以外、Null 終了、ASCII などです。既定で、P/Invoke サブシステムは、この記事で説明する既定の動作に基づいて適切な処理を実行しようと試みます。</span><span class="sxs-lookup"><span data-stu-id="d82cf-106">In managed code, for instance, you have a `String`, while in the unmanaged world strings can be Unicode ("wide"), non-Unicode, null-terminated, ASCII, etc. By default, the P/Invoke subsystem tries to do the right thing based on the default behavior, described on this article.</span></span> <span data-ttu-id="d82cf-107">しかし、追加の制御が必要な状況では、[MarshalAs](xref:System.Runtime.InteropServices.MarshalAsAttribute) 属性を採用して、アンマネージ側で期待する型を指定します。</span><span class="sxs-lookup"><span data-stu-id="d82cf-107">However, for those situations where you need extra control, you can employ the [MarshalAs](xref:System.Runtime.InteropServices.MarshalAsAttribute) attribute to specify what is the expected type on the unmanaged side.</span></span> <span data-ttu-id="d82cf-108">たとえば、文字列を null で終わる ANSI 文字列として送信させる場合は、次のように指定できます。</span><span class="sxs-lookup"><span data-stu-id="d82cf-108">For instance, if you want the string to be sent as a null-terminated ANSI string, you could do it like this:</span></span>

```csharp
[DllImport("somenativelibrary.dll")]
static extern int MethodA([MarshalAs(UnmanagedType.LPStr)] string parameter);
```

## <a name="default-rules-for-marshalling-common-types"></a><span data-ttu-id="d82cf-109">共通型をマーシャリングする場合の既定の規則</span><span class="sxs-lookup"><span data-stu-id="d82cf-109">Default rules for marshalling common types</span></span>

<span data-ttu-id="d82cf-110">一般的に、ランタイムは、マーシャリングするときにユーザーの必要な作業量が最小限になるように "適切な処理" を実行しようと試みます。</span><span class="sxs-lookup"><span data-stu-id="d82cf-110">Generally, the runtime tries to do the "right thing" when marshalling to require the least amount of work from you.</span></span> <span data-ttu-id="d82cf-111">次の表は、パラメーターまたはフィールドで使用されるときに、各型が既定でどのようにマーシャリングされるかを示しています。</span><span class="sxs-lookup"><span data-stu-id="d82cf-111">The following tables describe how each type is marshalled by default when used in a parameter or field.</span></span> <span data-ttu-id="d82cf-112">次の表がすべてのプラットフォームで正しくなるように、C99/C++ 11 固定幅の整数と文字型が使用されています。</span><span class="sxs-lookup"><span data-stu-id="d82cf-112">The C99/C++11 fixed-width integer and character types are used to ensure that the following table is correct for all platforms.</span></span> <span data-ttu-id="d82cf-113">このような型と同じ配置とサイズの要件を持つ任意のネイティブ型を使用できます。</span><span class="sxs-lookup"><span data-stu-id="d82cf-113">You can use any native type that has the same alignment and size requirements as these types.</span></span>

<span data-ttu-id="d82cf-114">この最初の表は、マーシャリングが P/Invoke とフィールド マーシャリングの両方で同じであるさまざまな型のマッピングを示しています。</span><span class="sxs-lookup"><span data-stu-id="d82cf-114">This first table describes the mappings for various types for whom the marshalling is the same for both P/Invoke and field marshalling.</span></span>

| <span data-ttu-id="d82cf-115">.NET 型</span><span class="sxs-lookup"><span data-stu-id="d82cf-115">.NET Type</span></span> | <span data-ttu-id="d82cf-116">ネイティブ型</span><span class="sxs-lookup"><span data-stu-id="d82cf-116">Native Type</span></span>  |
|-----------|-------------------------|
| `byte`    | `uint8_t`               |
| `sbyte`   | `int8_t`                |
| `short`   | `int16_t`               |
| `ushort`  | `uint16_t`              |
| `int`     | `int32_t`               |
| `uint`    | `uint32_t`              |
| `long`    | `int64_t`               |
| `ulong`   | `uint64_t`              |
| `char`    | <span data-ttu-id="d82cf-117">P/Invoke または構造体の `CharSet` に応じて、`char` または `char16_t` のいずれか。</span><span class="sxs-lookup"><span data-stu-id="d82cf-117">Either `char` or `char16_t` depending on the `CharSet` of the P/Invoke or structure.</span></span> <span data-ttu-id="d82cf-118">[文字セットのドキュメント](/.charset.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d82cf-118">See the [charset documentation](/.charset.md).</span></span> |
| `string`  | <span data-ttu-id="d82cf-119">P/Invoke または構造体の `CharSet` に応じて、`char*` または `char16_t*` のいずれか。</span><span class="sxs-lookup"><span data-stu-id="d82cf-119">Either `char*` or `char16_t*` depending on the `CharSet` of the P/Invoke or structure.</span></span> <span data-ttu-id="d82cf-120">[文字セットのドキュメント](/.charset.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d82cf-120">See the [charset documentation](/.charset.md).</span></span> |
| `System.IntPtr` | `intptr_t`        |
| `System.UIntPtr` | `uintptr_t`      |
| <span data-ttu-id="d82cf-121">.NET ポインター型 (例:</span><span class="sxs-lookup"><span data-stu-id="d82cf-121">.NET Pointer types (ex.</span></span> <span data-ttu-id="d82cf-122">`void*`)</span><span class="sxs-lookup"><span data-stu-id="d82cf-122">`void*`)</span></span>  | `void*` |
| <span data-ttu-id="d82cf-123">`System.Runtime.InteropServices.SafeHandle` の派生型</span><span class="sxs-lookup"><span data-stu-id="d82cf-123">Type derived from `System.Runtime.InteropServices.SafeHandle`</span></span> | `void*` |
| <span data-ttu-id="d82cf-124">`System.Runtime.InteropServices.CriticalHandle` の派生型</span><span class="sxs-lookup"><span data-stu-id="d82cf-124">Type derived from `System.Runtime.InteropServices.CriticalHandle`</span></span> | `void*`          |
| `bool`    | <span data-ttu-id="d82cf-125">Win32 `BOOL` 型</span><span class="sxs-lookup"><span data-stu-id="d82cf-125">Win32 `BOOL` type</span></span>       |
| `decimal` | <span data-ttu-id="d82cf-126">COM `DECIMAL` 構造体</span><span class="sxs-lookup"><span data-stu-id="d82cf-126">COM `DECIMAL` struct</span></span> |
| <span data-ttu-id="d82cf-127">.NET デリゲート</span><span class="sxs-lookup"><span data-stu-id="d82cf-127">.NET Delegate</span></span> | <span data-ttu-id="d82cf-128">ネイティブ関数ポインター</span><span class="sxs-lookup"><span data-stu-id="d82cf-128">Native function pointer</span></span> |
| `System.DateTime` | <span data-ttu-id="d82cf-129">Win32 `DATE` 型</span><span class="sxs-lookup"><span data-stu-id="d82cf-129">Win32 `DATE` type</span></span> |
| `System.Guid` | <span data-ttu-id="d82cf-130">Win32 `GUID` 型</span><span class="sxs-lookup"><span data-stu-id="d82cf-130">Win32 `GUID` type</span></span> |

<span data-ttu-id="d82cf-131">パラメーターまたは構造体としてマーシャリングする場合、マーシャリングの一部のカテゴリでは既定が異なります。</span><span class="sxs-lookup"><span data-stu-id="d82cf-131">A few categories of marshalling have different defaults if you're marshalling as a parameter or structure.</span></span>

| <span data-ttu-id="d82cf-132">.NET 型</span><span class="sxs-lookup"><span data-stu-id="d82cf-132">.NET Type</span></span> | <span data-ttu-id="d82cf-133">ネイティブ型 (パラメーター)</span><span class="sxs-lookup"><span data-stu-id="d82cf-133">Native Type (Parameter)</span></span> | <span data-ttu-id="d82cf-134">ネイティブ型 (フィールド)</span><span class="sxs-lookup"><span data-stu-id="d82cf-134">Native Type (Field)</span></span> |
|-----------|-------------------------|---------------------|
| <span data-ttu-id="d82cf-135">.NET 配列</span><span class="sxs-lookup"><span data-stu-id="d82cf-135">.NET array</span></span> | <span data-ttu-id="d82cf-136">配列要素のネイティブ表現の配列の先頭へのポインター。</span><span class="sxs-lookup"><span data-stu-id="d82cf-136">A pointer to the start of an array of native representations of the array elements.</span></span> | <span data-ttu-id="d82cf-137">使用するには `[MarshalAs]` 属性が必要です</span><span class="sxs-lookup"><span data-stu-id="d82cf-137">Not allowed without a `[MarshalAs]` attribute</span></span>|
| <span data-ttu-id="d82cf-138">`LayoutKind` が `Sequential` または `Explicit` のクラス</span><span class="sxs-lookup"><span data-stu-id="d82cf-138">A class with a `LayoutKind` of `Sequential` or `Explicit`</span></span> | <span data-ttu-id="d82cf-139">クラスのネイティブ表現へのポインター</span><span class="sxs-lookup"><span data-stu-id="d82cf-139">A pointer to the native representation of the class</span></span> | <span data-ttu-id="d82cf-140">クラスのネイティブ表現</span><span class="sxs-lookup"><span data-stu-id="d82cf-140">The native representation of the class</span></span> |

<span data-ttu-id="d82cf-141">次の表には、Windows のみの既定のマーシャリング規則が含まれています。</span><span class="sxs-lookup"><span data-stu-id="d82cf-141">The following table includes the default marshalling rules that are Windows-only.</span></span> <span data-ttu-id="d82cf-142">Windows 以外のプラットフォームでは、このような型をマーシャリングすることはできません。</span><span class="sxs-lookup"><span data-stu-id="d82cf-142">On non-Windows platforms, you cannot marshal these types.</span></span>

| <span data-ttu-id="d82cf-143">.NET 型</span><span class="sxs-lookup"><span data-stu-id="d82cf-143">.NET Type</span></span> | <span data-ttu-id="d82cf-144">ネイティブ型 (パラメーター)</span><span class="sxs-lookup"><span data-stu-id="d82cf-144">Native Type (Parameter)</span></span> | <span data-ttu-id="d82cf-145">ネイティブ型 (フィールド)</span><span class="sxs-lookup"><span data-stu-id="d82cf-145">Native Type (Field)</span></span> |
|-----------|-------------------------|---------------------|
| `object`  | `VARIANT`               | `IUnknown*`         |
| `System.Array` | <span data-ttu-id="d82cf-146">COM インターフェイス</span><span class="sxs-lookup"><span data-stu-id="d82cf-146">COM interface</span></span> | <span data-ttu-id="d82cf-147">使用するには `[MarshalAs]` 属性が必要です</span><span class="sxs-lookup"><span data-stu-id="d82cf-147">Not allowed without a `[MarshalAs]` attribute</span></span> |
| `System.ArgIterator` | `va_list` | <span data-ttu-id="d82cf-148">使用できません</span><span class="sxs-lookup"><span data-stu-id="d82cf-148">Not allowed</span></span> |
| `System.Collections.IEnumerator` | `IEnumVARIANT*` | <span data-ttu-id="d82cf-149">使用できません</span><span class="sxs-lookup"><span data-stu-id="d82cf-149">Not allowed</span></span> |
| `System.Collections.IEnumerable` | `IDispatch*` | <span data-ttu-id="d82cf-150">使用できません</span><span class="sxs-lookup"><span data-stu-id="d82cf-150">Not allowed</span></span> |
| `System.DateTimeOffset` | <span data-ttu-id="d82cf-151">1601 年 1 月 1 日午前 0 時以降のティック数を表す `int64_t`</span><span class="sxs-lookup"><span data-stu-id="d82cf-151">`int64_t` representing the number of ticks since midnight on January 1, 1601</span></span> || <span data-ttu-id="d82cf-152">1601 年 1 月 1 日午前 0 時以降のティック数を表す `int64_t`</span><span class="sxs-lookup"><span data-stu-id="d82cf-152">`int64_t` representing the number of ticks since midnight on January 1, 1601</span></span> |

<span data-ttu-id="d82cf-153">一部の型は、フィールドとしてではなくパラメーターとしてのみマーシャリングできます。</span><span class="sxs-lookup"><span data-stu-id="d82cf-153">Some types can only be marshalled as parameters and not as fields.</span></span> <span data-ttu-id="d82cf-154">このような型の一覧を次の表に示します。</span><span class="sxs-lookup"><span data-stu-id="d82cf-154">These types are listed in the following table:</span></span>

| <span data-ttu-id="d82cf-155">.NET 型</span><span class="sxs-lookup"><span data-stu-id="d82cf-155">.NET Type</span></span> | <span data-ttu-id="d82cf-156">ネイティブ型 (パラメーターのみ)</span><span class="sxs-lookup"><span data-stu-id="d82cf-156">Native Type (Parameter Only)</span></span> |
|-----------|------------------------------|
| `System.Text.StringBuilder` | <span data-ttu-id="d82cf-157">P/Invoke の `CharSet` に応じて、`char*` または `char16_t*` のいずれか。</span><span class="sxs-lookup"><span data-stu-id="d82cf-157">Either `char*` or `char16_t*` depending on the `CharSet` of the P/Invoke.</span></span>  <span data-ttu-id="d82cf-158">[文字セットのドキュメント](/.charset.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d82cf-158">See the [charset documentation](/.charset.md).</span></span> |
| `System.ArgIterator` | <span data-ttu-id="d82cf-159">`va_list` (Windows x86/x64/arm64 のみ)</span><span class="sxs-lookup"><span data-stu-id="d82cf-159">`va_list` (on Windows x86/x64/arm64 only)</span></span> |
| `System.Runtime.InteropServices.ArrayWithOffset` | `void*` |
| `System.Runtime.InteropServices.HandleRef` | `void*` |

<span data-ttu-id="d82cf-160">これらの既定値が目的と合わない場合は、パラメーターのマーシャリング方法をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="d82cf-160">If these defaults don't do exactly what you want, you can customize how parameters are marshalled.</span></span> <span data-ttu-id="d82cf-161">[パラメーターのマーシャリング](customize-parameter-marshalling.md)の記事では、さまざまなパラメーターの型をマーシャリングする方法のカスタマイズ手順について説明しています。</span><span class="sxs-lookup"><span data-stu-id="d82cf-161">The [parameter marshalling](customize-parameter-marshalling.md) article walks you through how to customize how different parameter types are marshalled.</span></span>

## <a name="marshalling-classes-and-structs"></a><span data-ttu-id="d82cf-162">クラスと構造体のマーシャリング</span><span class="sxs-lookup"><span data-stu-id="d82cf-162">Marshalling classes and structs</span></span>

<span data-ttu-id="d82cf-163">型のマーシャリングの別の側面は、構造体をアンマネージ メソッドに渡す方法です。</span><span class="sxs-lookup"><span data-stu-id="d82cf-163">Another aspect of type marshalling is how to pass in a struct to an unmanaged method.</span></span> <span data-ttu-id="d82cf-164">たとえば、一部のアンマネージ メソッドでは、パラメーターとして構造体が必要です。</span><span class="sxs-lookup"><span data-stu-id="d82cf-164">For instance, some of the unmanaged methods require a struct as a parameter.</span></span> <span data-ttu-id="d82cf-165">このような場合、環境のマネージド部分に対応する構造体またはクラスを作成し、それをパラメーターとして使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d82cf-165">In these cases, you need to create a corresponding struct or a class in managed part of the world to use it as a parameter.</span></span> <span data-ttu-id="d82cf-166">ただし、クラスを定義するだけでは不十分で、マーシャラーに、クラス内のフィールドをアンマネージ構造体にマップする方法を指示する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="d82cf-166">However, just defining the class isn't enough, you also need to instruct the marshaler how to map fields in the class to the unmanaged struct.</span></span> <span data-ttu-id="d82cf-167">ここで `StructLayout` 属性が役立ちます。</span><span class="sxs-lookup"><span data-stu-id="d82cf-167">Here the `StructLayout` attribute becomes useful.</span></span>

```csharp
[DllImport("kernel32.dll")]
static extern void GetSystemTime(SystemTime systemTime);

[StructLayout(LayoutKind.Sequential)]
class SystemTime {
    public ushort Year;
    public ushort Month;
    public ushort DayOfWeek;
    public ushort Day;
    public ushort Hour;
    public ushort Minute;
    public ushort Second;
    public ushort Milsecond;
}

public static void Main(string[] args) {
    SystemTime st = new SystemTime();
    GetSystemTime(st);
    Console.WriteLine(st.Year);
}
```

<span data-ttu-id="d82cf-168">上のコードは、`GetSystemTime()` 関数を呼び出す簡単な例を示しています。</span><span class="sxs-lookup"><span data-stu-id="d82cf-168">The previous code shows a simple example of calling into `GetSystemTime()` function.</span></span> <span data-ttu-id="d82cf-169">興味深いビットは 4 行目にあります。</span><span class="sxs-lookup"><span data-stu-id="d82cf-169">The interesting bit is on line 4.</span></span> <span data-ttu-id="d82cf-170">この属性は、他方 (アンマネージ) の側でクラスのフィールドを構造体に順番にマップする必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="d82cf-170">The attribute specifies that the fields of the class should be mapped sequentially to the struct on the other (unmanaged) side.</span></span> <span data-ttu-id="d82cf-171">このことは、次の例に示すアンマネージ構造体に対応する必要があるため、フィールドの名前付けは重要でなく、それらの順番だけが重要であることを意味します。</span><span class="sxs-lookup"><span data-stu-id="d82cf-171">This means that the naming of the fields isn't important, only their order is important, as it needs to correspond to the unmanaged struct, shown in the following example:</span></span>

```c
typedef struct _SYSTEMTIME {
  WORD wYear;
  WORD wMonth;
  WORD wDayOfWeek;
  WORD wDay;
  WORD wHour;
  WORD wMinute;
  WORD wSecond;
  WORD wMilliseconds;
} SYSTEMTIME, *PSYSTEMTIME*;
```

<span data-ttu-id="d82cf-172">構造体の既定のマーシャリングでは、必要な処理が実行されないことがあります。</span><span class="sxs-lookup"><span data-stu-id="d82cf-172">Sometimes the default marshalling for your structure doesn't do what you need.</span></span> <span data-ttu-id="d82cf-173">「[構造体のマーシャリングのカスタマイズ](./customize-struct-marshalling.md)」の記事では、構造体のマーシャリング方法をカスタマイズする手順が説明されています。</span><span class="sxs-lookup"><span data-stu-id="d82cf-173">The [Customizing structure marshalling](./customize-struct-marshalling.md) article teaches you how to customize how your structure is marshaled.</span></span>