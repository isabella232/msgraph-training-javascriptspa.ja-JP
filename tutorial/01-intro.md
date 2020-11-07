---
ms.openlocfilehash: bbb1dd429dca4e67735c5fdb2b2280f729115eb2
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822891"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="e584d-101">このチュートリアルでは、Microsoft Graph API を使用してユーザーの予定表情報を取得する、JavaScript のシングルページアプリを構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="e584d-101">This tutorial teaches you how to build a JavaScript single-page app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="e584d-102">完成したチュートリアルをダウンロードするだけで済む場合は、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-javascriptspa)をダウンロードするか、クローンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="e584d-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-javascriptspa).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e584d-103">前提条件</span><span class="sxs-lookup"><span data-stu-id="e584d-103">Prerequisites</span></span>

<span data-ttu-id="e584d-104">このチュートリアルを開始する前に、サンプルファイルをホストするための HTTP サーバーにアクセスする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e584d-104">Before you start this tutorial, you will need access to an HTTP server to host the sample files.</span></span> <span data-ttu-id="e584d-105">これは、開発コンピューター上のテストサーバー、またはリモートサーバーの場合があります。</span><span class="sxs-lookup"><span data-stu-id="e584d-105">This could be a test server on your development machine, or a remote server.</span></span> <span data-ttu-id="e584d-106">このチュートリアルでは、Node.js パッケージを使用して開発用のコンピューターで簡単なテストサーバーを実行する手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="e584d-106">The tutorial includes instructions to use a Node.js package to run a simple test server on your development machine.</span></span> <span data-ttu-id="e584d-107">このオプションを使用することを計画している場合は、開発用のコンピューターに [Node.js](https://nodejs.org) をインストールしておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="e584d-107">If you plan to use this option, you should have [Node.js](https://nodejs.org) installed on your development machine.</span></span> <span data-ttu-id="e584d-108">Node.js がない場合は、「ダウンロードオプション」の「前へ」のリンクを参照してください。</span><span class="sxs-lookup"><span data-stu-id="e584d-108">If you do not have Node.js, visit the previous link for download options.</span></span>

<span data-ttu-id="e584d-109">また、Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または Microsoft 職場または学校のアカウントを所有している必要があります。</span><span class="sxs-lookup"><span data-stu-id="e584d-109">You should also have either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span> <span data-ttu-id="e584d-110">Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="e584d-110">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="e584d-111">[新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。</span><span class="sxs-lookup"><span data-stu-id="e584d-111">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="e584d-112">[Office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="e584d-112">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e584d-113">このチュートリアルは、ノードバージョン12.16.1 を使用して作成されました。</span><span class="sxs-lookup"><span data-stu-id="e584d-113">This tutorial was written with Node version 12.16.1.</span></span> <span data-ttu-id="e584d-114">このガイドの手順は、他のバージョンでは動作しますが、テストされていません。</span><span class="sxs-lookup"><span data-stu-id="e584d-114">The steps in this guide may work with other versions, but that has not been tested.</span></span>

## <a name="feedback"></a><span data-ttu-id="e584d-115">フィードバック</span><span class="sxs-lookup"><span data-stu-id="e584d-115">Feedback</span></span>

<span data-ttu-id="e584d-116">このチュートリアルに関するフィードバックは、 [GitHub リポジトリ](https://github.com/microsoftgraph/msgraph-training-javascriptspa)に記入してください。</span><span class="sxs-lookup"><span data-stu-id="e584d-116">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-javascriptspa).</span></span>
