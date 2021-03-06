---
title: チャネル ファクトリとキャッシュ
ms.date: 03/30/2017
ms.assetid: 954f030e-091c-4c0e-a7a2-10f9a6b1f529
ms.openlocfilehash: 94b3cb22c76a215944d044db0f4392005e49f2ad
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645417"
---
# <a name="channel-factory-and-caching"></a>チャネル ファクトリとキャッシュ
WCF クライアント アプリケーションでは、<xref:System.ServiceModel.ChannelFactory%601> クラスを使用して WCF サービスとの通信チャネルを作成します。  <xref:System.ServiceModel.ChannelFactory%601> インスタンスを作成する場合は、次の操作が必要になるため、オーバーヘッドが生じます。  
  
- 構築、<xref:System.ServiceModel.Description.ContractDescription>ツリー  
  
- 必要なすべての CLR 型の反映  
  
- チャネル スタックの構築  
  
- リソースの破棄  
  
 このオーバーヘッドを最小限に抑えるために、WCF では、WCF クライアント プロキシの使用時にチャネル ファクトリをキャッシュできます。  
  
> [!TIP]
>  <xref:System.ServiceModel.ChannelFactory%601> クラスを直接使用する場合は、チャネル ファクトリの作成を直接制御できます。  
  
 WCF クライアント プロキシを使用して生成された[ServiceModel メタデータ ユーティリティ ツール (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)から派生<xref:System.ServiceModel.ClientBase%601>します。 <xref:System.ServiceModel.ClientBase%601> では、チャネル ファクトリのキャッシュ動作を定義する静的な <xref:System.ServiceModel.ClientBase%601.CacheSetting%2A> プロパティを定義します。 キャッシュ設定は特定の型に対して行われます。 たとえば、設定`ClientBase<ITest>.CacheSettings`以下に定義された値の 1 つにのみプロキシ/clientbase 型の影響は`ITest`します。 最初のプロキシ/ClientBase インスタンスが作成された時点で、特定の <xref:System.ServiceModel.ClientBase%601> のキャッシュ設定は不変になります。  
  
## <a name="specifying-caching-behavior"></a>キャッシュ動作の指定  
 キャッシュ動作は、<xref:System.ServiceModel.ClientBase%601.CacheSetting> プロパティを次のいずれかの値に設定することで指定します。  
  
|キャッシュの設定値|説明|  
|-------------------------|-----------------|  
|<xref:System.ServiceModel.CacheSetting.AlwaysOn>|アプリケーション ドメイン内の <xref:System.ServiceModel.ClientBase%601> のすべてのインスタンスはキャッシュに参加できます。 開発者は、セキュリティがキャッシュに悪影響を与えないことを確認しています。 キャッシュはオンになっていない場合、「セキュリティに影響する」でもプロパティをオフ<xref:System.ServiceModel.ClientBase%601>にアクセスします。 「セキュリティに影響する」プロパティ<xref:System.ServiceModel.ClientBase%601>は<xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A>、<xref:System.ServiceModel.ClientBase%601.Endpoint%2A>と<xref:System.ServiceModel.ClientBase%601.ChannelFactory%2A>します。|  
|<xref:System.ServiceModel.CacheSetting.Default>|構成ファイルで定義されているエンドポイントから作成された <xref:System.ServiceModel.ClientBase%601> のインスタンスのみがアプリケーション ドメイン内のキャッシュに参加します。 そのアプリケーション ドメイン内にプログラムで作成された <xref:System.ServiceModel.ClientBase%601> のインスタンスはキャッシュに参加しません。 また、キャッシュが無効になりますのインスタンス<xref:System.ServiceModel.ClientBase%601>の「セキュリティに影響する」プロパティにアクセスするとします。|  
|<xref:System.ServiceModel.CacheSetting.AlwaysOff>|対象となるアプリケーション ドメイン内にある特定の型の <xref:System.ServiceModel.ClientBase%601> のすべてのインスタンスのキャッシュが無効になります。|  
  
 <xref:System.ServiceModel.ClientBase%601.CacheSetting%2A> プロパティを使用する方法を次のコード スニペットに示します。  
  
```csharp  
class Program   
{   
   static void Main(string[] args)   
   {   
      ClientBase<ITest>.CacheSettings = CacheSettings.AlwaysOn;   
      foreach (string msg in messages)   
      {   
         using (TestClient proxy = new TestClient (new BasicHttpBinding(), new EndpointAddress(address)))   
         {   
            // ...  
            proxy.Test(msg);   
            // ...  
         }   
      }   
   }   
}  
// Generated by SvcUtil.exe     
public partial class TestClient : System.ServiceModel.ClientBase, ITest { }  
```  
  
 上のコードでは、`TestClient` のすべてのインスタンスで同じチャネル ファクトリを使用します。  
  
```csharp  
class Program   
{   
   static void Main(string[] args)   
   {   
      ClientBase.CacheSettings = CacheSettings.Default;   
      int i = 1;   
      foreach (string msg in messages)   
      {   
         using (TestClient proxy = new TestClient ("MyEndpoint", new EndpointAddress(address)))   
         {   
            if (i == 4)   
            {   
               ServiceEndpoint endpoint = proxy.Endpoint;   
               ... // use endpoint in some way   
            }   
            proxy.Test(msg);   
         }   
         i++;   
   }   
}   
  
// Generated by SvcUtil.exe     
public partial class TestClient : System.ServiceModel.ClientBase, ITest {}  
```  
  
 上の例では、`TestClient` のすべてのインスタンスで同じチャネル ファクトリを使用します (インスタンス #4 を除く)。 インスタンス #4 では、そのインスタンス専用に作成されたチャネル ファクトリを使用します。 この設定は、特定のエンドポイントで同じチャネル ファクトリ型 (この場合は `ITest`) の他のエンドポイントと異なるセキュリティ設定が必要なシナリオに有効です。  
  
```csharp  
class Program   
{   
   static void Main(string[] args)   
   {   
      ClientBase.CacheSettings = CacheSettings.AlwaysOff;   
      foreach (string msg in messages)   
      {   
         using (TestClient proxy = new TestClient ("MyEndpoint", new EndpointAddress(address)))   
         {   
            proxy.Test(msg);   
         }           
      }   
   }  
}  
  
// Generated by SvcUtil.exe   
public partial class TestClient : System.ServiceModel.ClientBase, ITest {}  
```  
  
 上の例では、`TestClient` のすべてのインスタンスで異なるチャネル ファクトリを使用します。 これは、エンドポイントごとにセキュリティ要件が異なり、キャッシュする意味がない場合に便利です。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.ClientBase%601>
- [クライアントを構築する](../../../../docs/framework/wcf/building-clients.md)
- [クライアント](../../../../docs/framework/wcf/feature-details/clients.md)
- [WCF クライアントを使用したサービスへのアクセス](../../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md)
- [方法: ChannelFactory を使用します。](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md)
