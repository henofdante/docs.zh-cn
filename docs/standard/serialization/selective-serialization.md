---
title: "有选择的序列化"
ms.date: 08/07/2017
ms.prod: .net
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- serialization, selective serialization
- binary serialization, selective serialization
ms.assetid: 39c56635-95d2-4afd-aff1-b022e7649bb3
caps.latest.revision: 6
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: 5cf437604f3072f3dec7b15897fcf5b6788289f0
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="selective-serialization"></a><span data-ttu-id="700bf-102">有选择的序列化</span><span class="sxs-lookup"><span data-stu-id="700bf-102">Selective serialization</span></span>
<span data-ttu-id="700bf-103">类通常包含不应进行序列化的字段。</span><span class="sxs-lookup"><span data-stu-id="700bf-103">A class often contains fields that shouldn't be serialized.</span></span> <span data-ttu-id="700bf-104">例如，假定类将线程 ID 存储在成员变量中。</span><span class="sxs-lookup"><span data-stu-id="700bf-104">For example, assume a class stores a thread ID in a member variable.</span></span> <span data-ttu-id="700bf-105">如果反序列化该类，而在对该类进行序列化时，存储了该 ID 的线程可能不再运行。因此，序列化该值毫无意义。</span><span class="sxs-lookup"><span data-stu-id="700bf-105">When the class is deserialized, the thread stored the ID for when the class was serialized might no longer be running; so serializing this value doesn't make sense.</span></span> <span data-ttu-id="700bf-106">按如下方法使用 [NonSerialized](xref:System.NonSerializedAttribute) 属性标记成员变量，可防止其被序列化。</span><span class="sxs-lookup"><span data-stu-id="700bf-106">You can prevent member variables from being serialized by marking them with the [NonSerialized](xref:System.NonSerializedAttribute) attribute as follows.</span></span>  
  
```csharp  
[Serializable]  
public class MyObject   
{  
  public int n1;  
  [NonSerialized] public int n2;  
  public String str;  
}  
```

<span data-ttu-id="700bf-107">如有可能，应使可能包含安全敏感数据的对象不可序列化。</span><span class="sxs-lookup"><span data-stu-id="700bf-107">If possible, make an object that could contain security-sensitive data nonserializable.</span></span> <span data-ttu-id="700bf-108">如果必须序列化该对象，则可将 `NonSerialized` 属性应用于存储敏感数据的特定字段。</span><span class="sxs-lookup"><span data-stu-id="700bf-108">If the object must be serialized, apply the `NonSerialized` attribute to specific fields that store sensitive data.</span></span> <span data-ttu-id="700bf-109">如果没有将这些字段排除在序列化之外，应该注意字段存储的数据会向有权序列化的所有代码公开。</span><span class="sxs-lookup"><span data-stu-id="700bf-109">If you don't exclude these fields from serialization, be aware that the data they store are exposed to any code that has permission to serialize.</span></span> <span data-ttu-id="700bf-110">有关编写安全的序列化代码的详细信息，请参阅[安全和序列化](../../../docs/framework/misc/security-and-serialization.md)。</span><span class="sxs-lookup"><span data-stu-id="700bf-110">For more information about writing secure serialization code, see [Security and Serialization](../../../docs/framework/misc/security-and-serialization.md).</span></span>

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]
  
## <a name="see-also"></a><span data-ttu-id="700bf-111">请参阅</span><span class="sxs-lookup"><span data-stu-id="700bf-111">See also</span></span>  
 <span data-ttu-id="700bf-112">[二进制序列化](binary-serialization.md) </span><span class="sxs-lookup"><span data-stu-id="700bf-112">[Binary Serialization](binary-serialization.md) </span></span>  
 <span data-ttu-id="700bf-113">[XML 和 SOAP 序列化](xml-and-soap-serialization.md) </span><span class="sxs-lookup"><span data-stu-id="700bf-113">[XML and SOAP Serialization](xml-and-soap-serialization.md) </span></span>  
 [<span data-ttu-id="700bf-114">安全性和序列化</span><span class="sxs-lookup"><span data-stu-id="700bf-114">Security and Serialization</span></span>](../../../docs/framework/misc/security-and-serialization.md)