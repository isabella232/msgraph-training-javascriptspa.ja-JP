---
ms.openlocfilehash: 77f74be505d72c6c0fd55d5f2650e32d03d63348
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822903"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="44cab-101">この演習では、Azure AD での認証をサポートするために、前の手順で作成したアプリケーションを拡張します。</span><span class="sxs-lookup"><span data-stu-id="44cab-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="44cab-102">これは、Microsoft Graph を呼び出すために必要な OAuth アクセストークンを取得するために必要です。</span><span class="sxs-lookup"><span data-stu-id="44cab-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="44cab-103">この手順では、アプリケーションに [Microsoft 認証ライブラリ](https://github.com/AzureAD/microsoft-authentication-library-for-js) ライブラリを統合します。</span><span class="sxs-lookup"><span data-stu-id="44cab-103">In this step you will integrate the [Microsoft Authentication Library](https://github.com/AzureAD/microsoft-authentication-library-for-js) library into the application.</span></span>

1. <span data-ttu-id="44cab-104">**config.js** という名前のルートディレクトリに新しいファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="44cab-104">Create a new file in the root directory named **config.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/config.example.js" id="msalConfigSnippet":::

    <span data-ttu-id="44cab-105">を `YOUR_APP_ID_HERE` アプリケーション登録ポータルからのアプリケーション ID に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="44cab-105">Replace `YOUR_APP_ID_HERE` with the application ID from the Application Registration Portal.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="44cab-106">Git などのソース管理を使用している場合は、アプリ ID を誤ってリークしないように、ソース管理から **config.js** ファイルを除外するのがよい時間になります。</span><span class="sxs-lookup"><span data-stu-id="44cab-106">If you're using source control such as git, now would be a good time to exclude the **config.js** file from source control to avoid inadvertently leaking your app ID.</span></span>

1. <span data-ttu-id="44cab-107">**auth.js** を開き、次のコードをファイルの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="44cab-107">Open **auth.js** and add the following code to the beginning of the file.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="authInitSnippet":::

## <a name="implement-sign-in"></a><span data-ttu-id="44cab-108">サインインの実装</span><span class="sxs-lookup"><span data-stu-id="44cab-108">Implement sign-in</span></span>

<span data-ttu-id="44cab-109">このセクションでは、 `signIn` 関数と関数を実装し `signOut` ます。</span><span class="sxs-lookup"><span data-stu-id="44cab-109">In this section you'll implement the `signIn` and `signOut` functions.</span></span>

1. <span data-ttu-id="44cab-110">既存の `signIn` 関数を、以下の関数で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="44cab-110">Replace the existing `signIn` function with the following.</span></span>

    ```javascript
    async function signIn() {
      // Login
      try {
        // Use MSAL to login
        const authResult = await msalClient.loginPopup(msalRequest);
        console.log('id_token acquired at: ' + new Date().toString());
        // Save the account username, needed for token acquisition
        sessionStorage.setItem('msalAccount', authResult.account.username);
        // TEMPORARY
        updatePage(Views.error, {
          message: 'Login successful',
          debug: `Token: ${authResult.accessToken}`
        });
      } catch (error) {
        console.log(error);
        updatePage(Views.error, {
          message: 'Error logging in',
          debug: error
        });
      }
    }
    ```

    <span data-ttu-id="44cab-111">この一時コードは、ログインが成功した後にアクセストークンを表示します。</span><span class="sxs-lookup"><span data-stu-id="44cab-111">This temporary code will display the access token after a successful login.</span></span>

1. <span data-ttu-id="44cab-112">既存の `signOut` 関数を、以下の関数で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="44cab-112">Replace the existing `signOut` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signOutSnippet":::

1. <span data-ttu-id="44cab-113">変更を保存してページを更新します。</span><span class="sxs-lookup"><span data-stu-id="44cab-113">Save your changes and refresh the page.</span></span> <span data-ttu-id="44cab-114">サインインした後、アクセストークンを示すエラーボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="44cab-114">After you sign in, you should see an error box that shows the access token.</span></span>

## <a name="get-the-users-profile"></a><span data-ttu-id="44cab-115">ユーザーのプロファイルを取得する</span><span class="sxs-lookup"><span data-stu-id="44cab-115">Get the user's profile</span></span>

<span data-ttu-id="44cab-116">このセクションでは、 `signIn` アクセストークンを使用して Microsoft Graph からユーザーのプロファイルを取得する機能を向上させます。</span><span class="sxs-lookup"><span data-stu-id="44cab-116">In this section you'll improve the `signIn` function to use the access token to get the user's profile from Microsoft Graph.</span></span>

1. <span data-ttu-id="44cab-117">ユーザーのアクセストークンを取得するには、 **auth.js** に次の関数を追加します。</span><span class="sxs-lookup"><span data-stu-id="44cab-117">Add the following function in **auth.js** to retrieve the user's access token.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="getTokenSnippet":::

1. <span data-ttu-id="44cab-118">**graph.js** という名前のプロジェクトのルートに新しいファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="44cab-118">Create a new file in the root of the project named **graph.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="graphInitSnippet":::

    <span data-ttu-id="44cab-119">このコードでは、メソッドをauth.jsにラップする承認プロバイダーを作成 `getToken` し、このプロバイダーを使用して \*\*\*\* Graph クライアントを初期化します。</span><span class="sxs-lookup"><span data-stu-id="44cab-119">This code creates an authorization provider that wraps the `getToken` method in **auth.js** , and initializes the Graph client with this provider.</span></span>

1. <span data-ttu-id="44cab-120">ユーザーのプロファイルを取得するには、 **graph.js** に次の関数を追加します。</span><span class="sxs-lookup"><span data-stu-id="44cab-120">Add the following function in **graph.js** to get the user's profile.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getUserSnippet":::

1. <span data-ttu-id="44cab-121">既存の `signIn` 関数を、以下の関数で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="44cab-121">Replace the existing `signIn` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signInSnippet":::

1. <span data-ttu-id="44cab-122">変更を保存してページを更新します。</span><span class="sxs-lookup"><span data-stu-id="44cab-122">Save your changes and refresh the page.</span></span> <span data-ttu-id="44cab-123">サインインした後は、ホームページに戻る必要がありますが、UI は、サインインしていることを示すように変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44cab-123">After you sign in, you should end up back on the home page, but the UI should change to indicate that you are signed-in.</span></span>

    ![サインイン後のホーム ページのスクリーンショット](./images/user-signed-in.png)

1. <span data-ttu-id="44cab-125">右上隅にあるユーザーアバターをクリックして、[ **サインアウト** ] リンクにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="44cab-125">Click the user avatar in the top right corner to access the **Sign out** link.</span></span> <span data-ttu-id="44cab-126">[ **サインアウト** ] をクリックすると、セッションがリセットされ、ホームページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="44cab-126">Clicking **Sign out** resets the session and returns you to the home page.</span></span>

    ![[サインアウト] リンクがあるドロップダウンメニューのスクリーンショット](./images/sign-out-button.png)

## <a name="storing-and-refreshing-tokens"></a><span data-ttu-id="44cab-128">トークンの格納と更新</span><span class="sxs-lookup"><span data-stu-id="44cab-128">Storing and refreshing tokens</span></span>

<span data-ttu-id="44cab-129">この時点で、アプリケーションには、API 呼び出しのヘッダーで送信されるアクセストークンがあり `Authorization` ます。</span><span class="sxs-lookup"><span data-stu-id="44cab-129">At this point your application has an access token, which is sent in the `Authorization` header of API calls.</span></span> <span data-ttu-id="44cab-130">これは、アプリがユーザーに代わって Microsoft Graph にアクセスできるようにするトークンです。</span><span class="sxs-lookup"><span data-stu-id="44cab-130">This is the token that allows the app to access the Microsoft Graph on the user's behalf.</span></span>

<span data-ttu-id="44cab-131">ただし、このトークンは一時的なものです。</span><span class="sxs-lookup"><span data-stu-id="44cab-131">However, this token is short-lived.</span></span> <span data-ttu-id="44cab-132">トークンが発行された後、有効期限が切れる時間になります。</span><span class="sxs-lookup"><span data-stu-id="44cab-132">The token expires an hour after it is issued.</span></span> <span data-ttu-id="44cab-133">ここで、更新トークンが役に立ちます。</span><span class="sxs-lookup"><span data-stu-id="44cab-133">This is where the refresh token becomes useful.</span></span> <span data-ttu-id="44cab-134">更新トークンを使用すると、ユーザーが再度サインインしなくても、アプリは新しいアクセス トークンを要求できます。</span><span class="sxs-lookup"><span data-stu-id="44cab-134">The refresh token allows the app to request a new access token without requiring the user to sign in again.</span></span>

<span data-ttu-id="44cab-135">アプリは MSAL ライブラリを使用しているため、トークンストレージを実装したり、ロジックを更新したりする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="44cab-135">Because the app is using the MSAL library, you do not have to implement any token storage or refresh logic.</span></span> <span data-ttu-id="44cab-136">MSAL は、ブラウザーセッションでトークンをキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="44cab-136">MSAL caches the token in the browser session.</span></span> <span data-ttu-id="44cab-137">この `acquireTokenSilent` メソッドは、最初にキャッシュされたトークンをチェックし、期限が切れていない場合はそれを返します。</span><span class="sxs-lookup"><span data-stu-id="44cab-137">The `acquireTokenSilent` method first checks the cached token, and if it is not expired, it returns it.</span></span> <span data-ttu-id="44cab-138">有効期限が切れている場合は、キャッシュされた更新トークンを使用して新しいものを取得します。</span><span class="sxs-lookup"><span data-stu-id="44cab-138">If it is expired, it uses the cached refresh token to obtain a new one.</span></span> <span data-ttu-id="44cab-139">Graph クライアントオブジェクトは、 `getToken` すべての要求について **auth.js** でメソッドを呼び出し、最新のトークンがあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="44cab-139">The Graph client object calls the `getToken` method in **auth.js** on every request, ensuring that it has an up-to-date token.</span></span>
