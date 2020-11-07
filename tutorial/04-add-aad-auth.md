---
ms.openlocfilehash: 77f74be505d72c6c0fd55d5f2650e32d03d63348
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822903"
---
<!-- markdownlint-disable MD002 MD041 -->

この演習では、Azure AD での認証をサポートするために、前の手順で作成したアプリケーションを拡張します。 これは、Microsoft Graph を呼び出すために必要な OAuth アクセストークンを取得するために必要です。 この手順では、アプリケーションに [Microsoft 認証ライブラリ](https://github.com/AzureAD/microsoft-authentication-library-for-js) ライブラリを統合します。

1. **config.js** という名前のルートディレクトリに新しいファイルを作成し、次のコードを追加します。

    :::code language="javascript" source="../demo/graph-tutorial/config.example.js" id="msalConfigSnippet":::

    を `YOUR_APP_ID_HERE` アプリケーション登録ポータルからのアプリケーション ID に置き換えます。

    > [!IMPORTANT]
    > Git などのソース管理を使用している場合は、アプリ ID を誤ってリークしないように、ソース管理から **config.js** ファイルを除外するのがよい時間になります。

1. **auth.js** を開き、次のコードをファイルの先頭に追加します。

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="authInitSnippet":::

## <a name="implement-sign-in"></a>サインインの実装

このセクションでは、 `signIn` 関数と関数を実装し `signOut` ます。

1. 既存の `signIn` 関数を、以下の関数で置き換えます。

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

    この一時コードは、ログインが成功した後にアクセストークンを表示します。

1. 既存の `signOut` 関数を、以下の関数で置き換えます。

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signOutSnippet":::

1. 変更を保存してページを更新します。 サインインした後、アクセストークンを示すエラーボックスが表示されます。

## <a name="get-the-users-profile"></a>ユーザーのプロファイルを取得する

このセクションでは、 `signIn` アクセストークンを使用して Microsoft Graph からユーザーのプロファイルを取得する機能を向上させます。

1. ユーザーのアクセストークンを取得するには、 **auth.js** に次の関数を追加します。

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="getTokenSnippet":::

1. **graph.js** という名前のプロジェクトのルートに新しいファイルを作成し、次のコードを追加します。

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="graphInitSnippet":::

    このコードでは、メソッドをauth.jsにラップする承認プロバイダーを作成 `getToken` し、このプロバイダーを使用して **** Graph クライアントを初期化します。

1. ユーザーのプロファイルを取得するには、 **graph.js** に次の関数を追加します。

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getUserSnippet":::

1. 既存の `signIn` 関数を、以下の関数で置き換えます。

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signInSnippet":::

1. 変更を保存してページを更新します。 サインインした後は、ホームページに戻る必要がありますが、UI は、サインインしていることを示すように変更する必要があります。

    ![サインイン後のホーム ページのスクリーンショット](./images/user-signed-in.png)

1. 右上隅にあるユーザーアバターをクリックして、[ **サインアウト** ] リンクにアクセスします。 [ **サインアウト** ] をクリックすると、セッションがリセットされ、ホームページに戻ります。

    ![[サインアウト] リンクがあるドロップダウンメニューのスクリーンショット](./images/sign-out-button.png)

## <a name="storing-and-refreshing-tokens"></a>トークンの格納と更新

この時点で、アプリケーションには、API 呼び出しのヘッダーで送信されるアクセストークンがあり `Authorization` ます。 これは、アプリがユーザーに代わって Microsoft Graph にアクセスできるようにするトークンです。

ただし、このトークンは一時的なものです。 トークンが発行された後、有効期限が切れる時間になります。 ここで、更新トークンが役に立ちます。 更新トークンを使用すると、ユーザーが再度サインインしなくても、アプリは新しいアクセス トークンを要求できます。

アプリは MSAL ライブラリを使用しているため、トークンストレージを実装したり、ロジックを更新したりする必要はありません。 MSAL は、ブラウザーセッションでトークンをキャッシュします。 この `acquireTokenSilent` メソッドは、最初にキャッシュされたトークンをチェックし、期限が切れていない場合はそれを返します。 有効期限が切れている場合は、キャッシュされた更新トークンを使用して新しいものを取得します。 Graph クライアントオブジェクトは、 `getToken` すべての要求について **auth.js** でメソッドを呼び出し、最新のトークンがあることを確認します。
