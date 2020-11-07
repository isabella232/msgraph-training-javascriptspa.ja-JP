---
ms.openlocfilehash: 0ef683278142776d6895b8655dd16e3635b90fa4
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822940"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="462c5-101">最初に、プロジェクト用の空のディレクトリを作成します。</span><span class="sxs-lookup"><span data-stu-id="462c5-101">Start by creating an empty directory for the project.</span></span> <span data-ttu-id="462c5-102">これは、HTTP サーバー、または開発コンピューター上のディレクトリにすることができます。</span><span class="sxs-lookup"><span data-stu-id="462c5-102">This can be on an HTTP server, or a directory on your development machine.</span></span> <span data-ttu-id="462c5-103">開発用コンピューター上にある場合は、テスト用にサーバーにコピーするか、開発用コンピューターで HTTP サーバーを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="462c5-103">If it is on your development machine, you'll need to copy it to a server for testing, or run an HTTP server on your development machine.</span></span> <span data-ttu-id="462c5-104">どちらの方法も使用していない場合は、次のセクションに指示が表示されます。</span><span class="sxs-lookup"><span data-stu-id="462c5-104">If you don't have either of those, the next section provides instructions.</span></span>

## <a name="start-a-local-web-server-optional"></a><span data-ttu-id="462c5-105">ローカル web サーバーを開始する (オプション)</span><span class="sxs-lookup"><span data-stu-id="462c5-105">Start a local web server (optional)</span></span>

> [!NOTE]
> <span data-ttu-id="462c5-106">このセクションの手順では [Node.js](https://nodejs.org)必要があります。</span><span class="sxs-lookup"><span data-stu-id="462c5-106">The steps in this section require [Node.js](https://nodejs.org).</span></span>

<span data-ttu-id="462c5-107">このセクションでは、 [http-server](https://www.npmjs.com/package/http-server) を使用して、コマンドラインから簡単な http サーバーを実行します。</span><span class="sxs-lookup"><span data-stu-id="462c5-107">In this section you will use [http-server](https://www.npmjs.com/package/http-server) to run a simple HTTP server from the command line.</span></span>

1. <span data-ttu-id="462c5-108">プロジェクト用に作成したディレクトリで、コマンドラインインターフェイス (CLI) を開きます。</span><span class="sxs-lookup"><span data-stu-id="462c5-108">Open your command-line interface (CLI) in the directory you created for the project.</span></span>
1. <span data-ttu-id="462c5-109">次のコマンドを実行して、そのディレクトリ内の web サーバーを起動します。</span><span class="sxs-lookup"><span data-stu-id="462c5-109">Run the following command to start a web server in that directory.</span></span>

    ```Shell
    npx http-server -c-1
    ```

1. <span data-ttu-id="462c5-110">ブラウザーを開き、を参照し `http://localhost:8080` ます。</span><span class="sxs-lookup"><span data-stu-id="462c5-110">Open your browser and browse to `http://localhost:8080`.</span></span>

<span data-ttu-id="462c5-111">**/Page のインデックス** が表示します。</span><span class="sxs-lookup"><span data-stu-id="462c5-111">You should see an **Index of /** page.</span></span> <span data-ttu-id="462c5-112">これにより、HTTP サーバーが実行中であることが確認されます。</span><span class="sxs-lookup"><span data-stu-id="462c5-112">This confirms that the HTTP server is running.</span></span>

![Http サーバーによって提供されるインデックスページのスクリーンショット。](images/run-web-server.png)

## <a name="design-the-app"></a><span data-ttu-id="462c5-114">アプリを設計する</span><span class="sxs-lookup"><span data-stu-id="462c5-114">Design the app</span></span>

<span data-ttu-id="462c5-115">このセクションでは、アプリケーション用の基本的な UI レイアウトを作成します。</span><span class="sxs-lookup"><span data-stu-id="462c5-115">In this section you'll create the basic UI layout for the application.</span></span>

1. <span data-ttu-id="462c5-116">プロジェクトのルートに **index.html** という名前の新しいファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="462c5-116">Create a new file in the root of the project named **index.html** and add the following code.</span></span>

    :::code language="html" source="../demo/graph-tutorial/index.html" id="indexSnippet":::

    <span data-ttu-id="462c5-117">これにより、ナビゲーションバーを含む、アプリの基本的なレイアウトが定義されます。</span><span class="sxs-lookup"><span data-stu-id="462c5-117">This defines the basic layout of the app, including a navigation bar.</span></span> <span data-ttu-id="462c5-118">また、次の項目も追加されます。</span><span class="sxs-lookup"><span data-stu-id="462c5-118">It also adds the following:</span></span>

    - <span data-ttu-id="462c5-119">[ブートストラップ](https://getbootstrap.com/) とそれをサポートする JavaScript</span><span class="sxs-lookup"><span data-stu-id="462c5-119">[Bootstrap](https://getbootstrap.com/) and its supporting JavaScript</span></span>
    - [<span data-ttu-id="462c5-120">FontAwesome</span><span class="sxs-lookup"><span data-stu-id="462c5-120">FontAwesome</span></span>](https://fontawesome.com/)
    - [<span data-ttu-id="462c5-121">Moment.js</span><span class="sxs-lookup"><span data-stu-id="462c5-121">Moment.js</span></span>](https://momentjs.com/)
    - [<span data-ttu-id="462c5-122">JavaScript の Microsoft 認証ライブラリ (MSAL.js) 2.0</span><span class="sxs-lookup"><span data-stu-id="462c5-122">Microsoft Authentication Library for JavaScript (MSAL.js) 2.0</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser)
    - [<span data-ttu-id="462c5-123">Microsoft Graph JavaScript クライアントライブラリ</span><span class="sxs-lookup"><span data-stu-id="462c5-123">Microsoft Graph JavaScript Client Library</span></span>](https://github.com/microsoftgraph/msgraph-sdk-javascript)

    > [!TIP]
    > <span data-ttu-id="462c5-124">ページには、favicon () が含まれてい `<link rel="shortcut icon" href="g-raph.png">` ます。</span><span class="sxs-lookup"><span data-stu-id="462c5-124">The page includes a favicon, (`<link rel="shortcut icon" href="g-raph.png">`).</span></span> <span data-ttu-id="462c5-125">この行を削除することも、 [GitHub](https://github.com/microsoftgraph/g-raph)から **g-raph.png** ファイルをダウンロードすることもできます。</span><span class="sxs-lookup"><span data-stu-id="462c5-125">You can remove this line, or you can download the **g-raph.png** file from [GitHub](https://github.com/microsoftgraph/g-raph).</span></span>

1. <span data-ttu-id="462c5-126">**スタイル .css** という名前の新しいファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="462c5-126">Create a new file named **style.css** and add the following code.</span></span>

    :::code language="css" source="../demo/graph-tutorial/style.css":::

1. <span data-ttu-id="462c5-127">**auth.js** という名前の新しいファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="462c5-127">Create a new file named **auth.js** and add the following code.</span></span>

    ```javascript
    function signIn() {
      // TEMPORARY
      updatePage({name: 'Megan Bowen', userName: 'meganb@contoso.com'});
    }

    function signOut() {
      // TEMPORARY
      updatePage();
    }
    ```

1. <span data-ttu-id="462c5-128">**ui.js** という名前の新しいファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="462c5-128">Create a new file named **ui.js** and add the following code.</span></span>

    ```javascript
    // Select DOM elements to work with
    const authenticatedNav = document.getElementById('authenticated-nav');
    const accountNav = document.getElementById('account-nav');
    const mainContainer = document.getElementById('main-container');

    const Views = { error: 1, home: 2, calendar: 3 };

    function createElement(type, className, text) {
      var element = document.createElement(type);
      element.className = className;

      if (text) {
        var textNode = document.createTextNode(text);
        element.appendChild(textNode);
      }

      return element;
    }

    function showAuthenticatedNav(user, view) {
      authenticatedNav.innerHTML = '';

      if (user) {
        // Add Calendar link
        var calendarNav = createElement('li', 'nav-item');

        var calendarLink = createElement('button',
          `btn btn-link nav-link${view === Views.calendar ? ' active' : '' }`,
          'Calendar');
        calendarLink.setAttribute('onclick', 'getEvents();');
        calendarNav.appendChild(calendarLink);

        authenticatedNav.appendChild(calendarNav);
      }
    }

    function showAccountNav(user) {
      accountNav.innerHTML = '';

      if (user) {
        // Show the "signed-in" nav
        accountNav.className = 'nav-item dropdown';

        var dropdown = createElement('a', 'nav-link dropdown-toggle');
        dropdown.setAttribute('data-toggle', 'dropdown');
        dropdown.setAttribute('role', 'button');
        accountNav.appendChild(dropdown);

        var userIcon = createElement('i',
          'far fa-user-circle fa-lg rounded-circle align-self-center');
        userIcon.style.width = '32px';
        dropdown.appendChild(userIcon);

        var menu = createElement('div', 'dropdown-menu dropdown-menu-right');
        dropdown.appendChild(menu);

        var userName = createElement('h5', 'dropdown-item-text mb-0', user.displayName);
        menu.appendChild(userName);

        var userEmail = createElement('p', 'dropdown-item-text text-muted mb-0', user.mail || user.userPrincipalName);
        menu.appendChild(userEmail);

        var divider = createElement('div', 'dropdown-divider');
        menu.appendChild(divider);

        var signOutButton = createElement('button', 'dropdown-item', 'Sign out');
        signOutButton.setAttribute('onclick', 'signOut();');
        menu.appendChild(signOutButton);
      } else {
        // Show a "sign in" button
        accountNav.className = 'nav-item';

        var signInButton = createElement('button', 'btn btn-link nav-link', 'Sign in');
        signInButton.setAttribute('onclick', 'signIn();');
        accountNav.appendChild(signInButton);
      }
    }

    function showWelcomeMessage(user) {
      // Create jumbotron
      var jumbotron = createElement('div', 'jumbotron');

      var heading = createElement('h1', null, 'JavaScript SPA Graph Tutorial');
      jumbotron.appendChild(heading);

      var lead = createElement('p', 'lead',
        'This sample app shows how to use the Microsoft Graph API to access' +
        ' a user\'s data from JavaScript.');
      jumbotron.appendChild(lead);

      if (user) {
        // Welcome the user by name
        var welcomeMessage = createElement('h4', null, `Welcome ${user.displayName}!`);
        jumbotron.appendChild(welcomeMessage);

        var callToAction = createElement('p', null,
          'Use the navigation bar at the top of the page to get started.');
        jumbotron.appendChild(callToAction);
      } else {
        // Show a sign in button in the jumbotron
        var signInButton = createElement('button', 'btn btn-primary btn-large',
          'Click here to sign in');
        signInButton.setAttribute('onclick', 'signIn();')
        jumbotron.appendChild(signInButton);
      }

      mainContainer.innerHTML = '';
      mainContainer.appendChild(jumbotron);
    }

    function showError(error) {
      var alert = createElement('div', 'alert alert-danger');

      var message = createElement('p', 'mb-3', error.message);
      alert.appendChild(message);

      if (error.debug)
      {
        var pre = createElement('pre', 'alert-pre border bg-light p-2');
        alert.appendChild(pre);

        var code = createElement('code', 'text-break text-wrap',
          JSON.stringify(error.debug, null, 2));
        pre.appendChild(code);
      }

      mainContainer.innerHTML = '';
      mainContainer.appendChild(alert);
    }

    function updatePage(view, data) {
      if (!view) {
        view = Views.home;
      }

      const user = JSON.parse(sessionStorage.getItem('graphUser'));

      showAccountNav(user);
      showAuthenticatedNav(user, view);

      switch (view) {
        case Views.error:
          showError(data);
          break;
        case Views.home:
          showWelcomeMessage(user);
          break;
        case Views.calendar:
          break;
      }
    }

    updatePage(Views.home);
    ```

1. <span data-ttu-id="462c5-129">すべての変更を保存し、ページを更新します。</span><span class="sxs-lookup"><span data-stu-id="462c5-129">Save all of your changes and refresh the page.</span></span> <span data-ttu-id="462c5-130">この時点で、アプリの外観は大きく異なります。</span><span class="sxs-lookup"><span data-stu-id="462c5-130">Now, the app should look very different.</span></span>

    ![デザインが変更されたホーム ページのスクリーンショット](images/app-layout.png)
