---
ms.openlocfilehash: 9b9b118c2d95710a5a3f9a1afe4d03a6185b4b14
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822933"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="c6c55-101">完了したプロジェクトを実行する方法</span><span class="sxs-lookup"><span data-stu-id="c6c55-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6c55-102">前提条件</span><span class="sxs-lookup"><span data-stu-id="c6c55-102">Prerequisites</span></span>

<span data-ttu-id="c6c55-103">このフォルダーで完了したプロジェクトを実行するには、次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="c6c55-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="c6c55-104">[Node.js](https://nodejs.org) 開発用コンピューターにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="c6c55-104">[Node.js](https://nodejs.org) installed on your development machine.</span></span> <span data-ttu-id="c6c55-105">Node.js がない場合は、「ダウンロードオプション」の「前へ」のリンクを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c6c55-105">If you do not have Node.js, visit the previous link for download options.</span></span> <span data-ttu-id="c6c55-106">( **注:** このチュートリアルは、ノードバージョン12.16.1 を使用して作成されています。</span><span class="sxs-lookup"><span data-stu-id="c6c55-106">( **Note:** This tutorial was written with Node version 12.16.1.</span></span> <span data-ttu-id="c6c55-107">このガイドの手順は、他のバージョンでは動作しますが、テストされていません。)</span><span class="sxs-lookup"><span data-stu-id="c6c55-107">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="c6c55-108">Outlook.com 上のメールボックスを持つ個人の Microsoft アカウント、または Microsoft 職場または学校のアカウントのいずれか。</span><span class="sxs-lookup"><span data-stu-id="c6c55-108">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="c6c55-109">Microsoft アカウントを持っていない場合は、無料のアカウントを取得するためのオプションがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="c6c55-109">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="c6c55-110">[新しい個人用 Microsoft アカウントにサインアップ](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)することができます。</span><span class="sxs-lookup"><span data-stu-id="c6c55-110">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="c6c55-111">[Office 365 開発者プログラムにサインアップ](https://developer.microsoft.com/office/dev-program)して、無料の office 365 サブスクリプションを取得することができます。</span><span class="sxs-lookup"><span data-stu-id="c6c55-111">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="c6c55-112">Web アプリケーションを Azure Active Directory 管理センターに登録する</span><span class="sxs-lookup"><span data-stu-id="c6c55-112">Register a web application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="c6c55-113">ブラウザーを開き、[Azure Active Directory 管理センター](https://aad.portal.azure.com)に移動します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-113">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="c6c55-114">**個人用アカウント** (別名: Microsoft アカウント)、または **職場/学校アカウント** を使用してログインします。</span><span class="sxs-lookup"><span data-stu-id="c6c55-114">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="c6c55-115">左側のナビゲーションで **[Azure Active Directory]** を選択し、それから **[管理]** で **[アプリの登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-115">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="c6c55-116">アプリの登録のスクリーンショット</span><span class="sxs-lookup"><span data-stu-id="c6c55-116">A screenshot of the App registrations</span></span> ](/tutorial/images/aad-portal-app-registrations.png)

    > <span data-ttu-id="c6c55-117">**注:** Azure AD B2C ユーザーには、 **アプリの登録 (レガシー)** だけが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="c6c55-117">**Note:** Azure AD B2C users may only see **App registrations (legacy)**.</span></span> <span data-ttu-id="c6c55-118">この場合は、に直接移動してください [https://aka.ms/appregistrations](https://aka.ms/appregistrations) 。</span><span class="sxs-lookup"><span data-stu-id="c6c55-118">In this case, please go directly to [https://aka.ms/appregistrations](https://aka.ms/appregistrations).</span></span>

1. <span data-ttu-id="c6c55-119">**[新規登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-119">Select **New registration**.</span></span> <span data-ttu-id="c6c55-120">**[アプリケーションを登録]** ページで、次のように値を設定します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-120">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="c6c55-121">`JavaScript Graph Tutorial` に **[名前]** を設定します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-121">Set **Name** to `JavaScript Graph Tutorial`.</span></span>
    - <span data-ttu-id="c6c55-122">**[サポートされているアカウントの種類]** を **[任意の組織のディレクトリ内のアカウントと個人用の Microsoft アカウント]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-122">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="c6c55-123">**[リダイレクト URI]** で、最初のドロップダウン リストを `Single-page application (SPA)` に設定し、それから `http://localhost:8080` に値を設定します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-123">Under **Redirect URI** , set the first drop-down to `Single-page application (SPA)` and set the value to `http://localhost:8080`.</span></span>

    ![[アプリケーションを登録する] ページのスクリーンショット](/tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="c6c55-125">**[登録]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-125">Choose **Register**.</span></span> <span data-ttu-id="c6c55-126">**JavaScript Graph のチュートリアル** ページで、 **アプリケーション (クライアント) ID** の値をコピーして保存します。次の手順で必要になります。</span><span class="sxs-lookup"><span data-stu-id="c6c55-126">On the **JavaScript Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![新しいアプリ登録のアプリケーション ID のスクリーンショット](/tutorial/images/aad-application-id.png)

1. <span data-ttu-id="c6c55-128">**[管理]** の下の **[認証]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-128">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="c6c55-129">暗黙的な **grant** セクションを見つけ、 **アクセストークン** と **ID トークン** を有効にします。</span><span class="sxs-lookup"><span data-stu-id="c6c55-129">Locate the **Implicit grant** section and enable **Access tokens** and **ID tokens**.</span></span> <span data-ttu-id="c6c55-130">**[保存]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-130">Choose **Save**.</span></span>

    ![[暗黙的な許可] セクションのスクリーンショット](/tutorial/images/aad-implicit-grant.png)

## <a name="configure-the-sample"></a><span data-ttu-id="c6c55-132">サンプルを構成する</span><span class="sxs-lookup"><span data-stu-id="c6c55-132">Configure the sample</span></span>

1. <span data-ttu-id="c6c55-133">**./Graph-tutorial/config.example.js** ファイルの名前を **/graph-tutorial/config.js** に変更します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-133">Rename the **./graph-tutorial/config.example.js** file to **./graph-tutorial/config.js**.</span></span>
1. <span data-ttu-id="c6c55-134">**/Graph-tutorial/config.js** ファイルを編集し、次のように変更します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-134">Edit the **./graph-tutorial/config.js** file and make the following changes.</span></span>
    1. <span data-ttu-id="c6c55-135">を `YOUR_APP_ID_HERE` アプリ登録ポータルで取得した **アプリケーション Id** に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c6c55-135">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="c6c55-136">サンプルを実行する</span><span class="sxs-lookup"><span data-stu-id="c6c55-136">Run the sample</span></span>

1. <span data-ttu-id="c6c55-137">CLI で次のコマンドを実行して、アプリケーションを起動します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-137">Run the following command in your CLI to start the application.</span></span>

    ```Shell
    npx http-server -c-1
    ```

1. <span data-ttu-id="c6c55-138">Web ブラウザーを開き、`http://localhost:8080` を参照します。</span><span class="sxs-lookup"><span data-stu-id="c6c55-138">Open a browser and browse to `http://localhost:8080`.</span></span>
