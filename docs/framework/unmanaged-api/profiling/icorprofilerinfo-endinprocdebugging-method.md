---
title: ICorProfilerInfo::EndInprocDebugging メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.EndInprocDebugging
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::EndInprocDebugging
helpviewer_keywords:
- ICorProfilerInfo::EndInprocDebugging method [.NET Framework profiling]
- EndInprocDebugging method [.NET Framework profiling]
ms.assetid: 35bc1188-9767-4141-8038-60ea015b99ac
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: bcae66fd30c29a0a3c9bd0b5ffc2047efdf3788d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62049662"
---
# <a name="icorprofilerinfoendinprocdebugging-method"></a>ICorProfilerInfo::EndInprocDebugging メソッド
プロセスでのデバッグ セッションを停止します。 このメソッドは、.NET Framework version 2.0 で廃止されています。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT EndInprocDebugging(  
    [in]  DWORD dwProfilerContext);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwProfilerContext`  
 [in]デバッグ セッションを識別する値。 この値はで受信したのと同じである必要があります、 [icorprofilerinfo::begininprocdebugging](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-begininprocdebugging-method.md)メソッド。  
  
## <a name="remarks"></a>Remarks  
 呼び出す必要があります[icorprofilerinfo::begininprocdebugging](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-begininprocdebugging-method.md)と`EndInprocDebugging`内、同じコールバック メソッド。  
  
 CLR デバッグ サービスでは、.NET Framework version 1.0 および 1.1 での制限、インプロセス デバッグがサポートされています。 インプロセス デバッグするには、デバッグ API の検査の部分を使用するプロファイラーを有効になっています。 ただし、お客様のフィードバックによりインプロセス デバッグが version 2.0、.NET Framework から削除され、プロファイル API に合わせてさらには、機能のセットに置き換えられます。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:**[システム要件](../../../../docs/framework/get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET framework のバージョン:** 1  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
