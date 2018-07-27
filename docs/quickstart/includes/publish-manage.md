<span data-ttu-id="a0fd8-101">从 nuget.org 上的配置文件中，选择“管理包”，查看刚刚发布的包。</span><span class="sxs-lookup"><span data-stu-id="a0fd8-101">From your profile on nuget.org, select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="a0fd8-102">同样也会收到确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="a0fd8-102">You also receive a confirmation email.</span></span> <span data-ttu-id="a0fd8-103">请注意，包可能需要一些时间才能编入索引并显示在可供他人查看的搜索结果中。</span><span class="sxs-lookup"><span data-stu-id="a0fd8-103">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="a0fd8-104">在该时间段，包页面会显示以下消息：</span><span class="sxs-lookup"><span data-stu-id="a0fd8-104">During that time your package page shows the message below:</span></span>

![此包未编制索引。](../media/QS_Create-03-NotIndexed.png)

<span data-ttu-id="a0fd8-107">就是这么简单！</span><span class="sxs-lookup"><span data-stu-id="a0fd8-107">And that's it!</span></span> <span data-ttu-id="a0fd8-108">刚刚已将第一个 NuGet 包发布到 nuget.org，其他开发人员可在自己的项目中使用它。</span><span class="sxs-lookup"><span data-stu-id="a0fd8-108">You've just published your first NuGet package to nuget.org that other developers can use in their own projects.</span></span>

<span data-ttu-id="a0fd8-109">如果你已在本演练中创建一个实际上并不使用的包（例如使用空的类库创建的包），则应取消列出将在搜索结果中隐藏的包：</span><span class="sxs-lookup"><span data-stu-id="a0fd8-109">If in this walkthrough you created a package that isn't actually useful (such as a package created with an empty class library), you should *unlist* the package to hide it from search results:</span></span>

1. <span data-ttu-id="a0fd8-110">在 nuget.org 上，选择用户名（在该页的右上角），然后选择“管理包”。</span><span class="sxs-lookup"><span data-stu-id="a0fd8-110">On nuget.org, select your user name (upper right of the page), then select **Manage Packages**.</span></span>

1. <span data-ttu-id="a0fd8-111">找到你需要在“已发布”下取消列出的包，然后选择右侧的回收站图标：</span><span class="sxs-lookup"><span data-stu-id="a0fd8-111">Locate the package you want to unlist under **Published** and select the trash can icon on the right:</span></span>

    ![在 nuget.org 上为包列表显示的回收站图标](../media/qs_create-vs-03-trash-can.png)

1. <span data-ttu-id="a0fd8-113">在随后的页面上，清除标记有“在搜索结果中列出(包名)”的框，然后选择“保存”：</span><span class="sxs-lookup"><span data-stu-id="a0fd8-113">On the subsequent page, clear the box labeled **List (package-name) in search results** and select **Save**:</span></span>

    ![在 nuget.org 上清除包的“列表”复选框](../media/qs_create-vs-04-unlist.png)