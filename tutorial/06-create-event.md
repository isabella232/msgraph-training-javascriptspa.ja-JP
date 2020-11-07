---
ms.openlocfilehash: 177f436812050ab4e9bf6c86bb5229b30f0f885b
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822952"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="7149b-101">このセクションでは、ユーザーの予定表にイベントを作成する機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="7149b-101">In this section you will add the ability to create events on the user's calendar.</span></span>

## <a name="create-a-new-event-form"></a><span data-ttu-id="7149b-102">新しいイベントフォームを作成する</span><span class="sxs-lookup"><span data-stu-id="7149b-102">Create a new event form</span></span>

1. <span data-ttu-id="7149b-103">次の関数を **ui.js** に追加して、新しいイベントのフォームをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="7149b-103">Add the following function to **ui.js** to render a form for the new event.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showNewEventFormSnippet":::

## <a name="create-the-event"></a><span data-ttu-id="7149b-104">イベントを作成する</span><span class="sxs-lookup"><span data-stu-id="7149b-104">Create the event</span></span>

1. <span data-ttu-id="7149b-105">次の関数を **graph.js** に追加して、フォームから値を読み取り、新しいイベントを作成します。</span><span class="sxs-lookup"><span data-stu-id="7149b-105">Add the following function to **graph.js** to read the values from the form and create a new event.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="createEventSnippet":::

1. <span data-ttu-id="7149b-106">変更を保存し、アプリを更新します。</span><span class="sxs-lookup"><span data-stu-id="7149b-106">Save your changes and refresh the app.</span></span> <span data-ttu-id="7149b-107">[ **予定表** ] ナビゲーション項目をクリックし、[ **イベントの作成** ] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7149b-107">Click the **Calendar** nav item, then click the **Create event** button.</span></span> <span data-ttu-id="7149b-108">値を入力し、[ **作成** ] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7149b-108">Fill in the values and click **Create**.</span></span> <span data-ttu-id="7149b-109">新しいイベントが作成されると、アプリは [予定表] ビューに戻ります。</span><span class="sxs-lookup"><span data-stu-id="7149b-109">The app returns to the calendar view once the new event is created.</span></span>

    ![新しいイベントフォームのスクリーンショット](images/create-event-01.png)
