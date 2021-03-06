---
title: サポートされているデプロイ シナリオ - WCF
ms.date: 03/30/2017
ms.assetid: 3399f208-3504-4c70-a22e-a7c02a8b94a6
ms.openlocfilehash: 986459e14206f073686474f5d65845ce682e1270
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2019
ms.locfileid: "65881057"
---
# <a name="supported-deployment-scenarios"></a>サポートされる展開シナリオ

部分的に信頼されたアプリケーションで使用するためにサポートされる Windows Communication Foundation (WCF) 機能のサブセットは、WCF を使用するが、一部のシナリオの要件を満たすために設計されています。 WCF がインターネット規模の要件を満たしているサード パーティ製のアプリケーションを実行しているホスティング プロバイダーの共有、サーバー上で、[!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)]中程度の信頼アクセス許可がセキュリティ上の理由を設定します。 クライアントでは、WCF の部分信頼サポートはなどの展開テクノロジの要件を満たすために設計[ClickOnce 配置](/visualstudio/deployment/clickonce-security-and-deployment)または[!INCLUDE[avalon2](../../../../includes/avalon2-md.md)]の XAML ブラウザー アプリケーションのテクノロジは、シームレスかつ安全に許可します。信頼されていないサイトからのデスクトップ アプリケーションの展開。

## <a name="minimum-permission-requirements"></a>最小権限の要件

WCF には、次の標準の名前付き権限セットのいずれかで実行されるアプリケーションの機能のサブセットがサポートされています。

- 中程度の信頼アクセス許可

- インターネット ゾーン アクセス許可

制限の厳しいアクセス許可が部分的に信頼されたアプリケーションで WCF を使用しようと、実行時にセキュリティ例外が発生する可能性があります。

このようなアクセス許可セットでサポートされる機能の詳細については、「 [Partial Trust Feature Compatibility](partial-trust-feature-compatibility.md)」を参照してください。

## <a name="partial-trust-on-the-server"></a>サーバーでの部分信頼

サービスをホストする ASP.NET Web アプリケーションの多くの商用プロバイダーは必須で、サーバーで実行されているアプリケーションが実行される、[!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)]中程度の信頼アクセス許可のセット。 使用する WCF サービスがこれらの環境で実行できる、 <xref:System.ServiceModel.BasicHttpBinding>、 <xref:System.ServiceModel.WebHttpBinding>、または<xref:System.ServiceModel.WSHttpBinding>トランスポート レベルのセキュリティ。

中程度の信頼ホスティング環境で実行されている WCF サービスは、クライアントの要求に応答の他のサーバーにメッセージを送信して中間層サービスとしても動作できます。 ホスティング環境が適切な <xref:System.Net.WebPermission> をアプリケーションに与えて、目的のサーバーに送信要求を行うようにする場合は、サーバーでの中間層のシナリオがサポートされます。

WCF がサポートしている SOAP メッセージングを使用して、サポートされている SOAP バインディングの 1 つだけでなく、<xref:System.ServiceModel.WebHttpBinding>部分的に信頼されたアプリケーションで Web スタイル サービスを構築するためです。 [WCF Web HTTP プログラミング モデル](wcf-web-http-programming-model.md)、 [WCF 配信](wcf-syndication.md)、および[AJAX の統合と JSON のサポート](ajax-integration-and-json-support.md)WCF の機能がすべて部分信頼でサポートされています。

ワークフロー サービスは完全信頼のアクセス許可を必要とし、部分的に信頼されたアプリケーションでは使用できません。

詳細については、「[方法 :ASP.NET 2.0 で中程度の信頼を使用して、](https://go.microsoft.com/fwlink/?LinkId=84603)します。

## <a name="partial-trust-on-the-client"></a>クライアントでの部分信頼

信頼されていないインターネット サイトからコードをダウンロードして実行する場合、ある程度のセキュリティ対策が必要です。 [ClickOnce 展開](/visualstudio/deployment/clickonce-security-and-deployment) と [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)]の XBAP テクノロジでは共に、部分信頼を利用して信頼できないコードに制限付きのアクセス許可 (インターネット ゾーン) を与えます。

WCF は、いずれかで展開された部分的に信頼されたアプリケーション内からリモート サーバーとの通信に使用できます[ClickOnce 配置](/visualstudio/deployment/clickonce-security-and-deployment)または XBAP します。 インターネット ゾーン アクセス許可のセットが含まれる<xref:System.Net.WebPermission>で説明されている、サポートされている WCF バインドのいずれかを使用して、配信元サーバーとの通信にこれらのアプリケーションの元のホスト用できる[Partial Trust Feature Compatibility](partial-trust-feature-compatibility.md).

## <a name="see-also"></a>関連項目

- [コード アクセス セキュリティ](../../misc/code-access-security.md)
- [WPF XAML ブラウザー アプリケーションの概要](../../wpf/app-development/wpf-xaml-browser-applications-overview.md)
- [部分信頼](partial-trust.md)
- [ASP.NET の信頼レベルとポリシー ファイル](https://docs.microsoft.com/previous-versions/wyts434y(v=vs.140))
