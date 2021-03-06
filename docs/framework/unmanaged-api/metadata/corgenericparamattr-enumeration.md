---
title: CorGenericParamAttr 列挙型
ms.date: 03/30/2017
api_name:
- CorGenericParamAttr
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorGenericParamAttr
helpviewer_keywords:
- CorGenericParamAttr enumeration [.NET Framework metadata]
ms.assetid: 36c76266-71d8-48dc-bd89-54943fa659c1
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0aa9b84c9e16811f799a3cd2ad096508db3f7d34
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62045791"
---
# <a name="corgenericparamattr-enumeration"></a>CorGenericParamAttr 列挙型
記述する値が含まれています、<xref:System.Type>の呼び出しで使用される、ジェネリック型パラメーター [imetadataemit 2::definegenericparam](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-definegenericparam-method.md)します。  
  
## <a name="syntax"></a>構文  
  
```  
typedef enum CorGenericParamAttr {  
  
    gpVarianceMask                     =   0x0003,  
    gpNonVariant                       =   0x0000,   
    gpCovariant                        =   0x0001,  
    gpContravariant                    =   0x0002,  
  
    gpSpecialConstraintMask            =   0x001C,  
    gpNoSpecialConstraint              =   0x0000,  
    gpReferenceTypeConstraint          =   0x0004,   
    gpNotNullableValueTypeConstraint   =   0x0008,  
    gpDefaultConstructorConstraint     =   0x0010  
  
} CorGenericParamAttr;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`gpVarianceMask`|パラメーターの分散は、インターフェイスおよびデリゲートのジェネリック パラメーターにのみ適用されます。|  
|`gpNonVariant`|差異がないことを示します。|  
|`gpCovariant`|共変性を示します。|  
|`gpContravariant`|反変性を示します。|  
|`gpSpecialConstraintMask`|特殊な制約は、いずれかに適用できる<xref:System.Type>パラメーター。|  
|`gpNoSpecialConstraint`|制約が適用されないことを示します、<xref:System.Type>パラメーター。|  
|`gpReferenceTypeConstraint`|示します、<xref:System.Type>パラメーターは参照型である必要があります。|  
|`gpNotNullableValueTypeConstraint`|示します、<xref:System.Type>パラメーターは null 値にすることはできません、値の型である必要があります。|  
|`gpDefaultConstructorConstraint`|示します、<xref:System.Type>パラメーターの既定のコンス トラクター パラメーターをとらない必要があります。|  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:**[システム要件](../../../../docs/framework/get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** CorHdr.h  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ列挙型](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
