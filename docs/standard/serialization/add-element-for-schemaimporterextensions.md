---
title: '&lt;追加&gt;要素&lt;schemaImporterExtensions&gt;'
ms.date: 03/30/2017
helpviewer_keywords:
- XML serialization, configuration
- <add> element for <schemaImporterExtensions> element
ms.assetid: c828a558-094b-441e-9065-790b87315fa0
ms.openlocfilehash: 3d3c72fd64042032d44c49ebde867d111ce03b94
ms.sourcegitcommit: efff8f331fd9467f093f8ab8d23a203d6ecb5b60
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/01/2018
ms.locfileid: "43453090"
---
# <a name="ltaddgt-element-for-ltschemaimporterextensionsgt"></a><span data-ttu-id="5c1e1-102">&lt;追加&gt;要素&lt;schemaImporterExtensions&gt;</span><span class="sxs-lookup"><span data-stu-id="5c1e1-102">&lt;add&gt; Element for &lt;schemaImporterExtensions&gt;</span></span>
<span data-ttu-id="5c1e1-103">XSD 型を .NET Framework 型に対応付けるために、<xref:System.Xml.Serialization.XmlSchemaImporter> によって使用される型を追加します。</span><span class="sxs-lookup"><span data-stu-id="5c1e1-103">Adds types used by the <xref:System.Xml.Serialization.XmlSchemaImporter> for mapping XSD types to .NET Framework types.</span></span> <span data-ttu-id="5c1e1-104">構成ファイルの詳細については、「[構成ファイル スキーマ](../../../docs/framework/configure-apps/file-schema/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5c1e1-104">For more information about configuration files, see [Configuration File Schema](../../../docs/framework/configure-apps/file-schema/index.md).</span></span>  
  
 <span data-ttu-id="5c1e1-105">\<configuration></span><span class="sxs-lookup"><span data-stu-id="5c1e1-105">\<configuration></span></span>  
<span data-ttu-id="5c1e1-106">\<system.xml.serialization></span><span class="sxs-lookup"><span data-stu-id="5c1e1-106">\<system.xml.serialization></span></span>  
<span data-ttu-id="5c1e1-107">\<schemaImporterExtensions></span><span class="sxs-lookup"><span data-stu-id="5c1e1-107">\<schemaImporterExtensions></span></span>  
<span data-ttu-id="5c1e1-108">\<add></span><span class="sxs-lookup"><span data-stu-id="5c1e1-108">\<add></span></span>  
  
## <a name="syntax"></a><span data-ttu-id="5c1e1-109">構文</span><span class="sxs-lookup"><span data-stu-id="5c1e1-109">Syntax</span></span>  
  
```xml  
<add name = "typeName" type="fully qualified type [,Version=version number] [,Culture=culture] [,PublicKeyToken= token]"/>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="5c1e1-110">属性および要素</span><span class="sxs-lookup"><span data-stu-id="5c1e1-110">Attributes and Elements</span></span>  
 <span data-ttu-id="5c1e1-111">以降のセクションでは、属性、子要素、および親要素について説明します。</span><span class="sxs-lookup"><span data-stu-id="5c1e1-111">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="5c1e1-112">属性</span><span class="sxs-lookup"><span data-stu-id="5c1e1-112">Attributes</span></span>  
  
|<span data-ttu-id="5c1e1-113">属性</span><span class="sxs-lookup"><span data-stu-id="5c1e1-113">Attribute</span></span>|<span data-ttu-id="5c1e1-114">説明</span><span class="sxs-lookup"><span data-stu-id="5c1e1-114">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="5c1e1-115">**name**</span><span class="sxs-lookup"><span data-stu-id="5c1e1-115">**name**</span></span>|<span data-ttu-id="5c1e1-116">インスタンスの検索に使用される簡易名。</span><span class="sxs-lookup"><span data-stu-id="5c1e1-116">A simple name that is used to find the instance.</span></span>|  
|<span data-ttu-id="5c1e1-117">**type**</span><span class="sxs-lookup"><span data-stu-id="5c1e1-117">**type**</span></span>|<span data-ttu-id="5c1e1-118">必須。</span><span class="sxs-lookup"><span data-stu-id="5c1e1-118">Required.</span></span> <span data-ttu-id="5c1e1-119">追加するスキーマ拡張クラスを指定します。</span><span class="sxs-lookup"><span data-stu-id="5c1e1-119">Specifies the schema  extension class to add.</span></span> <span data-ttu-id="5c1e1-120">**type** 属性の値は 1 行で指定し、完全修飾型名を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c1e1-120">The **type** attribute value must be on one line, and include the fully qualified type name.</span></span> <span data-ttu-id="5c1e1-121">アセンブリをグローバル アセンブリ キャッシュ (GAC: Global Assembly Cache) に配置する場合は、バージョン、カルチャ、およびアセンブリの署名に使用した公開キーのトークンも含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c1e1-121">When the assembly is placed in the Global Assembly Cache (GAC), it must also include the version, culture, and public key token of the signed assembly.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="5c1e1-122">子要素</span><span class="sxs-lookup"><span data-stu-id="5c1e1-122">Child Elements</span></span>  
 <span data-ttu-id="5c1e1-123">なし。</span><span class="sxs-lookup"><span data-stu-id="5c1e1-123">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="5c1e1-124">親要素</span><span class="sxs-lookup"><span data-stu-id="5c1e1-124">Parent Elements</span></span>  
  
|<span data-ttu-id="5c1e1-125">要素</span><span class="sxs-lookup"><span data-stu-id="5c1e1-125">Element</span></span>|<span data-ttu-id="5c1e1-126">説明</span><span class="sxs-lookup"><span data-stu-id="5c1e1-126">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="5c1e1-127">\<schemaImporterExtensions></span><span class="sxs-lookup"><span data-stu-id="5c1e1-127">\<schemaImporterExtensions></span></span>|<span data-ttu-id="5c1e1-128"><xref:System.Xml.Serialization.XmlSchemaImporter> によって使用される型が含まれます。</span><span class="sxs-lookup"><span data-stu-id="5c1e1-128">Contains the types that are used by the <xref:System.Xml.Serialization.XmlSchemaImporter>.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="5c1e1-129">例</span><span class="sxs-lookup"><span data-stu-id="5c1e1-129">Example</span></span>  
 <span data-ttu-id="5c1e1-130">型を対応付けるときに XmlSchemaImporter が使用できる拡張の型を追加するコード例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="5c1e1-130">The following code example adds an extension type that the XmlSchemaImporter can use when mapping types.</span></span>  
  
```xml  
<configuration>  
  <system.xml.serialization>  
    <schemaImporterExtensions>  
       <add name="contoso" type="System.Web.Mobile.MobileCapabilities,   
       System.Web.Mobile, Version=2.0.0.0, Culture=neutral,   
       PublicKeyToken=b03f5f7f11d50a3a" />   
    </schemaImporterExtensions>  
  </system.xml.serialization>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="5c1e1-131">関連項目</span><span class="sxs-lookup"><span data-stu-id="5c1e1-131">See Also</span></span>  
 <xref:System.Xml.Serialization.XmlSchemaImporter>  
 [<span data-ttu-id="5c1e1-132">\<system.xml.serialization> 要素</span><span class="sxs-lookup"><span data-stu-id="5c1e1-132">\<system.xml.serialization> Element</span></span>](../../../docs/standard/serialization/system-xml-serialization-element.md)  
 [<span data-ttu-id="5c1e1-133">\<schemaImporterExtensions> 要素</span><span class="sxs-lookup"><span data-stu-id="5c1e1-133">\<schemaImporterExtensions> Element</span></span>](../../../docs/standard/serialization/schemaimporterextensions-element.md)