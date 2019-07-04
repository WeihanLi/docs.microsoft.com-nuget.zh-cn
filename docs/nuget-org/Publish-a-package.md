---
title: 如何发布 NuGet 包
description: 详细说明如何将 NuGet 包发布到 nuget.org 或专用源，以及如何在 nuget.org 上管理包所有权。
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 6d183100a8319b517347567f34d276e94eb4e15d
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427182"
---
# <a name="publishing-packages"></a><span data-ttu-id="bcd61-103">发布包</span><span class="sxs-lookup"><span data-stu-id="bcd61-103">Publishing packages</span></span>

<span data-ttu-id="bcd61-104">创建程序包并获得 `.nupkg` 文件后，即可轻松以公开或私密方式将其提供给其他开发人员：</span><span class="sxs-lookup"><span data-stu-id="bcd61-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="bcd61-105">根据本文中的介绍，可通过 [nuget.org](https://www.nuget.org/packages/manage/upload) 将公共包全局提供给所有开发人员（需要 NuGet 4.1.0+）。</span><span class="sxs-lookup"><span data-stu-id="bcd61-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="bcd61-106">通过以下方式可以仅向团队或组织提供专用包：在文件共享、专用 NuGet 服务器、[Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) 或第三方存储库（如 myget、ProGet、Nexus 存储库和 Artifactory）上承载专用包。</span><span class="sxs-lookup"><span data-stu-id="bcd61-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="bcd61-107">有关其他详细信息，请参阅[承载包概述](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bcd61-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="bcd61-108">本文介绍如何发布到 nuget.org；有关发布到 Azure Artifacts 的信息，请参阅[包管理](https://www.visualstudio.com/docs/package/nuget/publish)。</span><span class="sxs-lookup"><span data-stu-id="bcd61-108">This article covers publishing to nuget.org; for publishing to Azure Artifacts, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="bcd61-109">发布到 nuget.org</span><span class="sxs-lookup"><span data-stu-id="bcd61-109">Publish to nuget.org</span></span>

<span data-ttu-id="bcd61-110">对于 nuget.org，必须使用 Microsoft 帐户进行登录，将需要在 nuget.org 中注册此帐户。此外可以使用较旧版本的门户创建的 nuget.org 帐户进行登录。</span><span class="sxs-lookup"><span data-stu-id="bcd61-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![NuGet 登录位置](media/publish_NuGetSignIn.png)

<span data-ttu-id="bcd61-112">接下来，可根据以下各节中的介绍，通过 nuget.org Web 门户上传包、从命令行（需要 `nuget.exe` 4.1.0+）将包推送到 nuget.org 或通过 Azure DevOps Services 在 CI/CD 过程中发布包。</span><span class="sxs-lookup"><span data-stu-id="bcd61-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Azure DevOps Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="bcd61-113">Web 门户：使用 nuget.org 上的“上传包”选项卡</span><span class="sxs-lookup"><span data-stu-id="bcd61-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="bcd61-114">选择 nuget.org 顶部菜单中的“上传”  ，并浏览到包位置。</span><span class="sxs-lookup"><span data-stu-id="bcd61-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![在 nuget.org 上上传包](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="bcd61-116">nuget.org 告知包名称是否可用。</span><span class="sxs-lookup"><span data-stu-id="bcd61-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="bcd61-117">如果无法使用，则更改项目中的包标识符、重新生成，并重试上传。</span><span class="sxs-lookup"><span data-stu-id="bcd61-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="bcd61-118">如果包名称可用，nuget.org 将打开“验证”  部分，可以在其中查看包清单中的元数据。</span><span class="sxs-lookup"><span data-stu-id="bcd61-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="bcd61-119">若要更改任何元数据，请编辑项目（项目文件或 `.nuspec` 文件）、重新生成、重新创建包，然后再次上传。</span><span class="sxs-lookup"><span data-stu-id="bcd61-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="bcd61-120">在“导入文档”  下，可以粘贴 Markdown、将 URL 指向文档，或上传文档文件。</span><span class="sxs-lookup"><span data-stu-id="bcd61-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="bcd61-121">当所有信息准备就绪后，选择“提交”  按钮</span><span class="sxs-lookup"><span data-stu-id="bcd61-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="bcd61-122">命令行</span><span class="sxs-lookup"><span data-stu-id="bcd61-122">Command line</span></span>

<span data-ttu-id="bcd61-123">若要将包推送到 nuget.org，必须使用实现所需 [NuGet 协议](../api/nuget-protocols.md)的 [nuget.exe v4.1.0 或更高版本](https://www.nuget.org/downloads)。</span><span class="sxs-lookup"><span data-stu-id="bcd61-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="bcd61-124">还需要在 nuget.org 上创建的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="bcd61-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="bcd61-125">创建 API 密钥</span><span class="sxs-lookup"><span data-stu-id="bcd61-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="bcd61-126">用 dotnet nuget push 发布</span><span class="sxs-lookup"><span data-stu-id="bcd61-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="bcd61-127">用 nuget push 发布</span><span class="sxs-lookup"><span data-stu-id="bcd61-127">Publish with nuget push</span></span>

1. <span data-ttu-id="bcd61-128">在命令提示符处运行以下命令，将 `<your_API_key>` 替换为从 nuget.org 获取的密钥：</span><span class="sxs-lookup"><span data-stu-id="bcd61-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="bcd61-129">此命令将 API 密钥存储在 NuGet 配置中，以便需要在同一台计算机上再次重复此步骤。</span><span class="sxs-lookup"><span data-stu-id="bcd61-129">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="bcd61-130">使用以下命令将包推送到 NuGet 库：</span><span class="sxs-lookup"><span data-stu-id="bcd61-130">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a><span data-ttu-id="bcd61-131">发布已签名的包</span><span class="sxs-lookup"><span data-stu-id="bcd61-131">Publish signed packages</span></span>

<span data-ttu-id="bcd61-132">若要提交已签名的包，必须首先[注册用于签名包的证书](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="bcd61-132">To submit signed packages, you must first [register the certificate](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) used for signing the packages.</span></span> 

> [!Warning]
> <span data-ttu-id="bcd61-133">nuget.org 会拒绝不满足[签名包要求](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)的包。</span><span class="sxs-lookup"><span data-stu-id="bcd61-133">nuget.org rejects packages that don't satisfy the [signed package requirements](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span></span>

### <a name="package-validation-and-indexing"></a><span data-ttu-id="bcd61-134">包验证和编制索引</span><span class="sxs-lookup"><span data-stu-id="bcd61-134">Package validation and indexing</span></span>

<span data-ttu-id="bcd61-135">推送到 nuget.org 的包会进行多项验证，如病毒检查。</span><span class="sxs-lookup"><span data-stu-id="bcd61-135">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="bcd61-136">（定期扫描 nuget.org 上的所有包。）</span><span class="sxs-lookup"><span data-stu-id="bcd61-136">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="bcd61-137">包通过所有验证检查后，对包编制索引并将其显示在搜索结果中可能需要一些时间。</span><span class="sxs-lookup"><span data-stu-id="bcd61-137">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="bcd61-138">编制索引完成后，你会收到一封确认已成功发布包的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="bcd61-138">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="bcd61-139">如果包未通过验证检查，将更新包详细信息页面以显示相关错误，同时你也会收到包含相关通知的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="bcd61-139">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="bcd61-140">包验证和编制索引所需的时间通常不超过 15 分钟。</span><span class="sxs-lookup"><span data-stu-id="bcd61-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="bcd61-141">如果发布包所用时间超出预期，请访问 [status.nuget.org](https://status.nuget.org/) 检查 nuget.org 是否遇到任何中断。</span><span class="sxs-lookup"><span data-stu-id="bcd61-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="bcd61-142">如果所有系统均正常运行，但一个小时之内还未成功发布包，请登录 nuget.org 并使用包页面上的“联系支持人员”链接与我们联系。</span><span class="sxs-lookup"><span data-stu-id="bcd61-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="bcd61-143">若要查看包状态，请选择 nuget.org 上帐户名称下的“管理包”  。完成验证时，会收到确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="bcd61-143">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="bcd61-144">请注意，对包编制索引并将其显示在搜索结果中供其他人查找可能需要一些时间。在此期间，包页面上会出现以下消息：</span><span class="sxs-lookup"><span data-stu-id="bcd61-144">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![指示尚未发布包的消息](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a><span data-ttu-id="bcd61-146">Azure DevOps Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="bcd61-146">Azure DevOps Services (CI/CD)</span></span>

<span data-ttu-id="bcd61-147">如果在持续集成/部署过程中使用 Azure DevOps Services 将包推送到 nuget.org，必须在 NuGet 任务中使用 `nuget.exe` 4.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="bcd61-147">If you push packages to nuget.org using Azure DevOps Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="bcd61-148">要了解详细信息，请参阅 [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/)（在生成中使用最新 NuGet）（Microsoft DevOps 博客）。</span><span class="sxs-lookup"><span data-stu-id="bcd61-148">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="bcd61-149">在 nuget.org 上管理包所有者</span><span class="sxs-lookup"><span data-stu-id="bcd61-149">Managing package owners on nuget.org</span></span>

<span data-ttu-id="bcd61-150">尽管每个 NuGet 包的 `.nuspec` 文件定义了该包的创建者，但 nuget.org 库不使用该元数据定义所有权。</span><span class="sxs-lookup"><span data-stu-id="bcd61-150">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="bcd61-151">相反，nuget.org 将初始所有权分配给发布包的人员。</span><span class="sxs-lookup"><span data-stu-id="bcd61-151">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="bcd61-152">他们通常是通过 nuget.org UI 上传包的已登录用户，或其 API 密钥与 `nuget SetApiKey` 或 `nuget push` 配合使用的用户。</span><span class="sxs-lookup"><span data-stu-id="bcd61-152">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="bcd61-153">所有包所有者均拥有包的完全权限，包括添加和删除其他所有者以及发布更新。</span><span class="sxs-lookup"><span data-stu-id="bcd61-153">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="bcd61-154">要更改包的所有权，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="bcd61-154">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="bcd61-155">使用包的当前所有者的帐户登录 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="bcd61-155">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="bcd61-156">选择帐户名称，选择“管理包”  ，然后展开“已发布的包”  。</span><span class="sxs-lookup"><span data-stu-id="bcd61-156">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="bcd61-157">选择要管理的包，然后在右侧选择“管理所有者”  。</span><span class="sxs-lookup"><span data-stu-id="bcd61-157">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="bcd61-158">此时，你具有多个选择：</span><span class="sxs-lookup"><span data-stu-id="bcd61-158">From here you have several options:</span></span>

1. <span data-ttu-id="bcd61-159">删除“当前所有者”  下列出的任何所有者。</span><span class="sxs-lookup"><span data-stu-id="bcd61-159">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="bcd61-160">在“添加所有者”  下添加所有者，方法是通过输入其用户名和一条消息，然后选择“添加”  。</span><span class="sxs-lookup"><span data-stu-id="bcd61-160">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="bcd61-161">此操作会向该新共有者发送包含确认链接的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="bcd61-161">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="bcd61-162">确认后，此人拥有添加和删除所有者的完全权限。</span><span class="sxs-lookup"><span data-stu-id="bcd61-162">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="bcd61-163">（确认之前，“当前所有者”  部分指示此人的状态为“待审批”。）</span><span class="sxs-lookup"><span data-stu-id="bcd61-163">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="bcd61-164">要转让所有权（如变更所有权或在错误的帐户下发布包时），请添加新所有者，他们确认所有权后，即可将你从列表中删除。</span><span class="sxs-lookup"><span data-stu-id="bcd61-164">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="bcd61-165">要将所有权分配给公司或组，请使用转发到适当团队成员的电子邮件别名创建 nuget.org 帐户。</span><span class="sxs-lookup"><span data-stu-id="bcd61-165">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="bcd61-166">例如，各种 Microsoft ASP.NET 包由 [microsoft](http://nuget.org/profiles/microsoft) 和 [aspnet](http://nuget.org/profiles/aspnet) 帐户共同拥有，这两个帐户就是此类别名。</span><span class="sxs-lookup"><span data-stu-id="bcd61-166">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="bcd61-167">恢复包的所有权</span><span class="sxs-lookup"><span data-stu-id="bcd61-167">Recovering package ownership</span></span>

<span data-ttu-id="bcd61-168">有时，包所有者可能不太活跃。</span><span class="sxs-lookup"><span data-stu-id="bcd61-168">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="bcd61-169">例如，原始所有者可能已离开生产该包的公司，nuget.org 凭据丢失，或库中的早期 bug 导致包不具有所有者。</span><span class="sxs-lookup"><span data-stu-id="bcd61-169">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="bcd61-170">如果你是包的合法所有者且需要重新获得所有权，请使用 nuget.org 上的[联系表单](https://www.nuget.org/policies/Contact)向 NuGet 团队解释相关情况。</span><span class="sxs-lookup"><span data-stu-id="bcd61-170">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="bcd61-171">然后，我们按照流程验证你对包的所有权，包括通过包的项目 URL、Twitter、电子邮件或其他方式尝试找出现有所有者。</span><span class="sxs-lookup"><span data-stu-id="bcd61-171">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="bcd61-172">但如果所有其他方式均失败，我们会向你发送成为所有者的邀请。</span><span class="sxs-lookup"><span data-stu-id="bcd61-172">But if all else fails, we can send you a new invite to become an owner.</span></span>