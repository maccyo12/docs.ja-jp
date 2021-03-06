---
title: グラフィックスについて
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [Windows Forms], using managed interface
- graphics [Windows Forms], about graphics
ms.assetid: a602aef8-a8c8-4c36-9816-74e7bad96a68
ms.openlocfilehash: 927fc327d9ad42cd3a99af207d04efbc520df8b5
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645700"
---
# <a name="overview-of-graphics"></a>グラフィックスについて
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] Microsoft Windows オペレーティング システムのサブシステムを形成するアプリケーション プログラミング インターフェイス (API) です。 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 情報を表示する画面およびプリンターを担当します。 その名前からわかるように、[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] は [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] の後継であり、以前のバージョンの Windows に含まれているグラフィックス デバイス インターフェイスです。  
  
## <a name="managed-class-interface"></a>マネージド クラスのインターフェイス  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] API はマネージ コードとして配置されているクラスのセットを通じて公開します。 このクラスのセットと呼ばれる、*マネージ クラスのインターフェイス*に[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]します。 次の名前空間は、マネージド クラスのインターフェイスを構成します。  
  
- <xref:System.Drawing>  
  
- <xref:System.Drawing.Drawing2D>  
  
- <xref:System.Drawing.Imaging>  
  
- <xref:System.Drawing.Text>  
  
- <xref:System.Drawing.Printing>  
  
 グラフィックス デバイス インターフェイスを備えたなど[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]、画面またはプリンターの情報を表示するには、特定のディスプレイ デバイスの詳細について心配する必要はありません。 プログラマは [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] クラスによって提供されるさまざまなメソッドを呼び出します。 次に、これらのメソッドで、特定のデバイス ドライバーへの適切な呼び出しを実行します。 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] は、グラフィックス ハードウェアからアプリケーションを分離します。 この分離により、プログラマはデバイスに依存しないアプリケーションを作成することをお勧めします。  
  
## <a name="see-also"></a>関連項目

- [グラフィックスの概要](graphics-overview-windows-forms.md)
