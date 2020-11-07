---
ms.openlocfilehash: 1f2ff0e013bd1b104cd5b353ba2da542382657ab
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822945"
---
<!-- markdownlint-disable MD002 MD041 -->

この演習では、Microsoft Graph をアプリケーションに組み込みます。 このアプリケーションでは、microsoft graph [JavaScript クライアントライブラリ](https://github.com/microsoftgraph/msgraph-sdk-javascript) ライブラリを使用して、microsoft graph を呼び出すことにします。

## <a name="get-calendar-events-from-outlook"></a>Outlook からカレンダー イベントを取得する

このセクションでは、Microsoft Graph クライアントライブラリを使用して、ユーザーの予定表イベントを取得します。

1. **timezones.js** という名前のプロジェクトのルートに新しいファイルを作成し、次のコードを追加します。

    :::code language="javascript" source="../demo/graph-tutorial/timezones.js" id="zoneMappingsSnippet":::

    このコードでは、Windows タイムゾーン識別子を IANA タイムゾーン識別子にマップ moment.js との互換性を確保します。

1. **graph.js** に次の関数を追加します。

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getEventsSnippet":::

    このコードの実行内容を考えましょう。

    - 呼び出される URL は `/me/calendarview` です。
    - この `header` メソッドは、 `Prefer` ユーザーの優先タイムゾーンを指定するヘッダーを追加します。
    - この `query` メソッドは、予定表ビューの開始時刻と終了時刻を追加します。
    - `select`このメソッドは、各イベントに対して返されるフィールドを、ビューが実際に使用するものだけに制限します。
    - メソッドは、 `orderby` 開始時刻で結果を並べ替えます。最も古いイベントは最初になります。
    - メソッドは、 `top` 応答で最大50イベントを要求します。

1. **ui.js** を開いて、次の関数を追加します。

    ```javascript
    function showCalendar(events) {
      // TEMPORARY
      // Render the results as JSON
      var alert = createElement('div', 'alert alert-success');

      var pre = createElement('pre', 'alert-pre border bg-light p-2');
      alert.appendChild(pre);

      var code = createElement('code', 'text-break',
        JSON.stringify(events, null, 2));
      pre.appendChild(code);

      mainContainer.innerHTML = '';
      mainContainer.appendChild(alert);
    }
    ```

1. `switch`ビューがである場合に呼び出す関数のステートメントを更新 `updatePage` `showCalendar` `Views.calendar` します。

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="updatePageSnippet" highlight="18-20":::

1. 変更を保存し、アプリを更新します。 サインインして、ナビゲーションバーの [ **予定表** ] リンクをクリックします。 すべてが正常に機能していれば、ユーザーのカレンダーにイベントの JSON ダンプが表示されます。

## <a name="display-the-results"></a>結果の表示

このセクションでは、関数を更新して、 `showCalendar` よりわかりやすい方法でイベントを表示します。

1. 既存の `showCalendar` 関数を、以下の関数で置き換えます。

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showCalendarSnippet":::

    これにより、イベントのコレクションがループ処理され、テーブル行が1つずつ追加されます。

1. 変更を保存し、アプリを更新します。 [ **予定表** ] リンクをクリックすると、現在の週のイベントの表が表示されるようになります。

    ![イベント表のスクリーンショット](./images/calendar-list.png)
