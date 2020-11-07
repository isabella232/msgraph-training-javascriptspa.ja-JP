---
ms.openlocfilehash: 177f436812050ab4e9bf6c86bb5229b30f0f885b
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822952"
---
<!-- markdownlint-disable MD002 MD041 -->

このセクションでは、ユーザーの予定表にイベントを作成する機能を追加します。

## <a name="create-a-new-event-form"></a>新しいイベントフォームを作成する

1. 次の関数を **ui.js** に追加して、新しいイベントのフォームをレンダリングします。

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showNewEventFormSnippet":::

## <a name="create-the-event"></a>イベントを作成する

1. 次の関数を **graph.js** に追加して、フォームから値を読み取り、新しいイベントを作成します。

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="createEventSnippet":::

1. 変更を保存し、アプリを更新します。 [ **予定表** ] ナビゲーション項目をクリックし、[ **イベントの作成** ] ボタンをクリックします。 値を入力し、[ **作成** ] をクリックします。 新しいイベントが作成されると、アプリは [予定表] ビューに戻ります。

    ![新しいイベントフォームのスクリーンショット](images/create-event-01.png)
