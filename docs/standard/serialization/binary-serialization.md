---
title: "二进制序列化"
ms.date: 08/11/2017
ms.prod: .net
ms.topic: article
helpviewer_keywords:
- binary serialization
- serialization, about serialization
- deserialization
- binary serialization, about serialization
- binary serialization, .net core serialization
- serialization, cross-framework
ms.assetid: 2b1ea3be-1152-4032-b2b3-07794054c405
caps.latest.revision: 5
author: ViktorHofer
ms.author: mairaw
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: 995430b2426cb124ee889ed49cc7260c68138151
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="binary-serialization"></a><span data-ttu-id="efbb7-102">二进制序列化</span><span class="sxs-lookup"><span data-stu-id="efbb7-102">Binary serialization</span></span>

<span data-ttu-id="efbb7-103">可以将序列化定义为一个将对象状态存储到存储介质的过程。</span><span class="sxs-lookup"><span data-stu-id="efbb7-103">Serialization can be defined as the process of storing the state of an object to a storage medium.</span></span> <span data-ttu-id="efbb7-104">在这个过程中，对象的公共字段和私有字段以及类（包括含有该类的程序集）的名称，将转换成字节流，而字节流接着将写入数据流。</span><span class="sxs-lookup"><span data-stu-id="efbb7-104">During this process, the public and private fields of the object and the name of the class, including the assembly containing the class, are converted to a stream of bytes, which is then written to a data stream.</span></span> <span data-ttu-id="efbb7-105">随后对该对象进行反序列化时，将创建原始对象的准确克隆。</span><span class="sxs-lookup"><span data-stu-id="efbb7-105">When the object is subsequently deserialized, an exact clone of the original object is created.</span></span>

<span data-ttu-id="efbb7-106">在面向对象的环境中实现序列化机制时，必须多在易用性与灵活性之间做出权衡。</span><span class="sxs-lookup"><span data-stu-id="efbb7-106">When implementing a serialization mechanism in an object-oriented environment, you have to make a number of tradeoffs between ease of use and flexibility.</span></span> <span data-ttu-id="efbb7-107">很大程度上，这个过程可以自动完成，但前提是您对该过程拥有足够的控制权。</span><span class="sxs-lookup"><span data-stu-id="efbb7-107">The process can be automated to a large extent, provided you are given sufficient control over the process.</span></span> <span data-ttu-id="efbb7-108">例如，如果简单的二进制序列化不足，或者可能有特定原因决定需要对类中的哪些字段进行序列化，可能就会出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="efbb7-108">For example, situations may arise where simple binary serialization is not sufficient, or there might be a specific reason to decide which fields in a class need to be serialized.</span></span> <span data-ttu-id="efbb7-109">以下章节验证了随 .NET Framework 一起提供的可靠序列化机制，并强调了根据需要自定义该过程所能使用的一些重要功能。</span><span class="sxs-lookup"><span data-stu-id="efbb7-109">The following sections examine the robust serialization mechanism provided with .NET and highlight a number of important features that allow you to customize the process to meet your needs.</span></span>

> [!NOTE]
> <span data-ttu-id="efbb7-110">如果使用不同的 .NET Framework 版本序列化和反序列化以 UTF-8 或 UTF-7 编码的对象，则不保留该对象的状态。</span><span class="sxs-lookup"><span data-stu-id="efbb7-110">The state of a UTF-8 or UTF-7 encoded object is not preserved if the object is serialized and deserialized using different .NET Framework versions.</span></span>

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]

<span data-ttu-id="efbb7-111">由于二进制序列化的性质允许在对象内修改私有成员，因此若要更改其状态，建议使用其他序列化框架，如在公共 API 曲面上操作的 JSON.NET。</span><span class="sxs-lookup"><span data-stu-id="efbb7-111">As the nature of binary serialization allows the modification of private members inside an object and therefore changing the state of it, other serialization frameworks like JSON.NET which operate on the public API surface are recommended.</span></span>

## <a name="binary-serialization-in-net-core"></a><span data-ttu-id="efbb7-112">.NET Core 中的二进制序列化</span><span class="sxs-lookup"><span data-stu-id="efbb7-112">Binary serialization in .NET Core</span></span>

<span data-ttu-id="efbb7-113">.NET Core 支持带有类型子集的二进制序列化。</span><span class="sxs-lookup"><span data-stu-id="efbb7-113">.NET Core supports binary serialization with a subset of types.</span></span> <span data-ttu-id="efbb7-114">可在[可序列化类型部分](#serializable-types)查看受支持的类型列表。</span><span class="sxs-lookup"><span data-stu-id="efbb7-114">You can see the list of supported types in the [Serializable types section](#serializable-types).</span></span> <span data-ttu-id="efbb7-115">一组已定义的类型是完全可以在 .NET Framework 4.5.1 及更高版本之间和 .NET Core 2.0 及更高版本之间进行序列化的。</span><span class="sxs-lookup"><span data-stu-id="efbb7-115">The defined set of types are guaranteed to be serializable between .NET Framework 4.5.1 and later versions and .NET Core 2.0 and later versions.</span></span> <span data-ttu-id="efbb7-116">其他 .NET 实现（如 Mono）并未正式得到支持，但应该也能使用。</span><span class="sxs-lookup"><span data-stu-id="efbb7-116">Other .NET implementations, such as Mono, aren't officially supported but should also be working.</span></span>

### <a name="serializable-types"></a><span data-ttu-id="efbb7-117">可序列化类型</span><span class="sxs-lookup"><span data-stu-id="efbb7-117">Serializable types</span></span>

- <xref:System.AggregateException?displayProperty=fullName>   
- <xref:System.Array?displayProperty=fullName>   
- <xref:System.ArraySegment%601?displayProperty=fullName>   
- <xref:System.Attribute?displayProperty=fullName>   
- <xref:System.Boolean?displayProperty=fullName>   
- <xref:System.Byte?displayProperty=fullName>   
- <xref:System.Char?displayProperty=fullName>   
- <xref:System.Collections.ArrayList?displayProperty=fullName>   
- <xref:System.Collections.BitArray?displayProperty=fullName>   
- <xref:System.Collections.Comparer?displayProperty=fullName>   
- <xref:System.Collections.DictionaryEntry?displayProperty=fullName>   
- <xref:System.Collections.Generic.Comparer%601?displayProperty=fullName>   
- <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName>   
- <xref:System.Collections.Generic.EqualityComparer%601?displayProperty=fullName>   
- <xref:System.Collections.Generic.HashSet%601?displayProperty=fullName>   
- <xref:System.Collections.Generic.KeyValuePair%602?displayProperty=fullName>   
- <xref:System.Collections.Generic.LinkedList%601?displayProperty=fullName>   
- <xref:System.Collections.Generic.List%601?displayProperty=fullName>   
- <xref:System.Collections.Generic.Queue%601?displayProperty=fullName>   
- <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=fullName>   
- <xref:System.Collections.Generic.SortedList%602?displayProperty=fullName>   
- <xref:System.Collections.Generic.SortedSet%601?displayProperty=fullName>   
- <xref:System.Collections.Generic.Stack%601?displayProperty=fullName>   
- <xref:System.Collections.Hashtable?displayProperty=fullName>   
- <xref:System.Collections.ObjectModel.Collection%601?displayProperty=fullName>   
- <xref:System.Collections.ObjectModel.KeyedCollection%602?displayProperty=fullName>   
- <xref:System.Collections.ObjectModel.ObservableCollection%601?displayProperty=fullName>   
- <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=fullName>   
- <xref:System.Collections.ObjectModel.ReadOnlyDictionary%602?displayProperty=fullName>   
- <xref:System.Collections.ObjectModel.ReadOnlyObservableCollection%601?displayProperty=fullName>   
- <xref:System.Collections.Queue?displayProperty=fullName>   
- <xref:System.Collections.SortedList?displayProperty=fullName>   
- <xref:System.Collections.Specialized.HybridDictionary?displayProperty=fullName>   
- <xref:System.Collections.Specialized.ListDictionary?displayProperty=fullName>   
- <xref:System.Collections.Specialized.OrderedDictionary?displayProperty=fullName>   
- <xref:System.Collections.Specialized.StringCollection?displayProperty=fullName>   
- <xref:System.Collections.Specialized.StringDictionary?displayProperty=fullName>   
- <xref:System.Collections.Stack?displayProperty=fullName>   
- <xref:System.ComponentModel.BindingList%601?displayProperty=fullName>   
- <xref:System.Data.DataSet?displayProperty=fullName>   
- <xref:System.Data.DataTable?displayProperty=fullName>   
- <xref:System.Data.PropertyCollection?displayProperty=fullName>   
- <xref:System.Data.SqlTypes.SqlBoolean?displayProperty=fullName>   
- <xref:System.Data.SqlTypes.SqlByte?displayProperty=fullName>   
- <xref:System.Data.SqlTypes.SqlDateTime?displayProperty=fullName>   
- <xref:System.Data.SqlTypes.SqlDouble?displayProperty=fullName>   
- <xref:System.Data.SqlTypes.SqlGuid?displayProperty=fullName>   
- <xref:System.Data.SqlTypes.SqlInt16?displayProperty=fullName>   
- <xref:System.Data.SqlTypes.SqlInt32?displayProperty=fullName>   
- <xref:System.Data.SqlTypes.SqlInt64?displayProperty=fullName>   
- <xref:System.Data.SqlTypes.SqlString?displayProperty=fullName>   
- <xref:System.DateTime?displayProperty=fullName>   
- <xref:System.DateTimeOffset?displayProperty=fullName>   
- <xref:System.Decimal?displayProperty=fullName>   
- <xref:System.Double?displayProperty=fullName>   
- <xref:System.Drawing.Color?displayProperty=fullName>   
- <xref:System.Drawing.Point?displayProperty=fullName>   
- <xref:System.Drawing.PointF?displayProperty=fullName>   
- <xref:System.Drawing.Rectangle?displayProperty=fullName>   
- <xref:System.Drawing.RectangleF?displayProperty=fullName>   
- <xref:System.Drawing.Size?displayProperty=fullName>   
- <xref:System.Drawing.SizeF?displayProperty=fullName>   
- <xref:System.Enum?displayProperty=fullName>   
- <xref:System.Exception?displayProperty=fullName>   
- <xref:System.Globalization.CompareInfo?displayProperty=fullName>   
- <xref:System.Globalization.SortVersion?displayProperty=fullName>   
- <xref:System.Guid?displayProperty=fullName>   
- <xref:System.Int16?displayProperty=fullName>   
- <xref:System.Int32?displayProperty=fullName>   
- <xref:System.Int64?displayProperty=fullName>   
- <xref:System.IntPtr?displayProperty=fullName>   
- <xref:System.Net.Cookie?displayProperty=fullName>   
- <xref:System.Net.CookieCollection?displayProperty=fullName>   
- <xref:System.Net.CookieContainer?displayProperty=fullName>   
- <xref:System.Nullable%601?displayProperty=fullName>   
- <xref:System.Numerics.BigInteger?displayProperty=fullName>   
- <xref:System.Numerics.Complex?displayProperty=fullName>   
- <xref:System.Object?displayProperty=fullName>   
- <xref:System.SByte?displayProperty=fullName>   
- <xref:System.Single?displayProperty=fullName>   
- <xref:System.String?displayProperty=fullName>   
- <xref:System.StringComparer?displayProperty=fullName>   
- <xref:System.Text.StringBuilder?displayProperty=fullName>   
- <xref:System.TimeSpan?displayProperty=fullName>   
- <xref:System.TimeZoneInfo?displayProperty=fullName>   
- <xref:System.TimeZoneInfo.AdjustmentRule?displayProperty=fullName>   
- <xref:System.Tuple?displayProperty=fullName>   
- <xref:System.UInt16?displayProperty=fullName>   
- <xref:System.UInt32?displayProperty=fullName>   
- <xref:System.UInt64?displayProperty=fullName>   
- <xref:System.UIntPtr?displayProperty=fullName>   
- <xref:System.Uri?displayProperty=fullName>   
- <xref:System.ValueTuple?displayProperty=fullName>   
- <xref:System.ValueType?displayProperty=fullName>   
- <xref:System.Version?displayProperty=fullName>   
- <xref:System.WeakReference?displayProperty=fullName>   
- <xref:System.WeakReference%601?displayProperty=fullName>   

## <a name="in-this-section"></a><span data-ttu-id="efbb7-118">本节内容</span><span class="sxs-lookup"><span data-stu-id="efbb7-118">In this section</span></span>

 [<span data-ttu-id="efbb7-119">序列化概念</span><span class="sxs-lookup"><span data-stu-id="efbb7-119">Serialization Concepts</span></span>](../../../docs/standard/serialization/serialization-concepts.md)  
 <span data-ttu-id="efbb7-120">讨论序列化在其中有用的两种方案：在将数据保持到存储中以及在跨应用程序域传递对象时。</span><span class="sxs-lookup"><span data-stu-id="efbb7-120">Discusses two scenarios where serialization is useful: when persisting data to storage and when passing objects across application domains.</span></span>  
  
 [<span data-ttu-id="efbb7-121">基本序列化</span><span class="sxs-lookup"><span data-stu-id="efbb7-121">Basic Serialization</span></span>](../../../docs/standard/serialization/basic-serialization.md)  
 <span data-ttu-id="efbb7-122">描述如何使用二进制格式化程序和 SOAP 格式化程序来序列化对象。</span><span class="sxs-lookup"><span data-stu-id="efbb7-122">Describes how to use the binary and SOAP formatters to serialize objects.</span></span>  
  
 [<span data-ttu-id="efbb7-123">有选择的序列化</span><span class="sxs-lookup"><span data-stu-id="efbb7-123">Selective Serialization</span></span>](../../../docs/standard/serialization/selective-serialization.md)  
 <span data-ttu-id="efbb7-124">描述如何防止序列化某些类成员。</span><span class="sxs-lookup"><span data-stu-id="efbb7-124">Describes how to prevent some members of a class from being serialized.</span></span>  
  
 [<span data-ttu-id="efbb7-125">自定义序列化</span><span class="sxs-lookup"><span data-stu-id="efbb7-125">Custom Serialization</span></span>](../../../docs/standard/serialization/custom-serialization.md)  
 <span data-ttu-id="efbb7-126">描述如何使用 <xref:System.Runtime.Serialization.ISerializable> 接口自定义类的序列化。</span><span class="sxs-lookup"><span data-stu-id="efbb7-126">Describes how to customize serialization for a class by using the <xref:System.Runtime.Serialization.ISerializable> interface.</span></span>  
  
 [<span data-ttu-id="efbb7-127">序列化过程中的步骤</span><span class="sxs-lookup"><span data-stu-id="efbb7-127">Steps in the Serialization Process</span></span>](../../../docs/standard/serialization/steps-in-the-serialization-process.md)  
 <span data-ttu-id="efbb7-128">描述对格式化程序调用 <xref:System.Runtime.Serialization.Formatter.Serialize%2A> 方法时序列化采取操作的过程。</span><span class="sxs-lookup"><span data-stu-id="efbb7-128">Describes the course of action serialization takes when the <xref:System.Runtime.Serialization.Formatter.Serialize%2A> method is called on a formatter.</span></span>  
  
 [<span data-ttu-id="efbb7-129">版本容错序列化</span><span class="sxs-lookup"><span data-stu-id="efbb7-129">Version Tolerant Serialization</span></span>](../../../docs/standard/serialization/version-tolerant-serialization.md)  
 <span data-ttu-id="efbb7-130">介绍如何创建可序列化类型。在不导致应用程序引发异常的情况下，可以在以后对这样的类型进行修改。</span><span class="sxs-lookup"><span data-stu-id="efbb7-130">Explains how to create serializable types that can be modified over time without causing applications to throw exceptions.</span></span>  
  
 [<span data-ttu-id="efbb7-131">序列化准则</span><span class="sxs-lookup"><span data-stu-id="efbb7-131">Serialization Guidelines</span></span>](../../../docs/standard/serialization/serialization-guidelines.md)  
 <span data-ttu-id="efbb7-132">提供一些通用准则，用于确定何时序列化对象。</span><span class="sxs-lookup"><span data-stu-id="efbb7-132">Provides some general guidelines for deciding when to serialize an object.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="efbb7-133">参考</span><span class="sxs-lookup"><span data-stu-id="efbb7-133">Reference</span></span>  
 <xref:System.Runtime.Serialization>  
 <span data-ttu-id="efbb7-134">包含可用于序列化和反序列化对象的类。</span><span class="sxs-lookup"><span data-stu-id="efbb7-134">Contains classes that can be used for serializing and deserializing objects.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="efbb7-135">相关章节</span><span class="sxs-lookup"><span data-stu-id="efbb7-135">Related sections</span></span>  
 [<span data-ttu-id="efbb7-136">XML 和 SOAP 序列化</span><span class="sxs-lookup"><span data-stu-id="efbb7-136">XML and SOAP Serialization</span></span>](../../../docs/standard/serialization/xml-and-soap-serialization.md)  
 <span data-ttu-id="efbb7-137">描述随公共语言运行库一起提供的 XML 序列化机制。</span><span class="sxs-lookup"><span data-stu-id="efbb7-137">Describes the XML serialization mechanism that is included with the common language runtime.</span></span>  
  
 [<span data-ttu-id="efbb7-138">安全性和序列化</span><span class="sxs-lookup"><span data-stu-id="efbb7-138">Security and Serialization</span></span>](../../../docs/framework/misc/security-and-serialization.md)  
 <span data-ttu-id="efbb7-139">描述写入执行序列化的代码时需要遵循的安全编码原则。</span><span class="sxs-lookup"><span data-stu-id="efbb7-139">Describes the secure coding guidelines to follow when writing code that performs serialization.</span></span>  
  
 [<span data-ttu-id="efbb7-140">远程对象</span><span class="sxs-lookup"><span data-stu-id="efbb7-140">Remote Objects</span></span>](http://msdn.microsoft.com/en-us/515686e6-0a8d-42f7-8188-73abede57c58)  
 <span data-ttu-id="efbb7-141">描述 .NET Framework 中为远程通信提供的多种通信方法。</span><span class="sxs-lookup"><span data-stu-id="efbb7-141">Describes the various communications methods available in the .NET Framework for remote communications.</span></span>  
  
 [<span data-ttu-id="efbb7-142">使用 ASP.NET 创建的 XML Web service 以及 XML Web Service 客户端</span><span class="sxs-lookup"><span data-stu-id="efbb7-142">XML Web Services Created Using ASP.NET and XML Web Service Clients</span></span>](http://msdn.microsoft.com/en-us/1e64af78-d705-4384-b08d-591a45f4379c)  
 <span data-ttu-id="efbb7-143">提供一些主题，描述并解释如何对使用 ASP.NET 创建的 XML Web services 进行编程。</span><span class="sxs-lookup"><span data-stu-id="efbb7-143">Provides topics that describe and explain how to program XML Web services created using ASP.NET.</span></span>
