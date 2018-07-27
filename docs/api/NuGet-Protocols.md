---
title: nuget.org 协议
description: 不断发展与 NuGet 客户端交互 nuget.org 协议。
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: cc6d52617ea8b69d5b18b831ddf8a1a85dd6798f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822573"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="29e22-103">nuget.org 协议</span><span class="sxs-lookup"><span data-stu-id="29e22-103">nuget.org protocols</span></span>

<span data-ttu-id="29e22-104">若要与 nuget.org 进行交互，客户端需要遵循某些协议。</span><span class="sxs-lookup"><span data-stu-id="29e22-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="29e22-105">由于这些协议保留在发展，客户端必须标识调用特定 nuget.org Api 时，他们使用的协议版本。</span><span class="sxs-lookup"><span data-stu-id="29e22-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="29e22-106">这允许 nuget.org 的旧客户端的非换行方式引入的更改。</span><span class="sxs-lookup"><span data-stu-id="29e22-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="29e22-107">此页上介绍的 Api 是特定于 nuget.org 并且没有其他的 NuGet 服务器实现引入这些 Api 不期望。</span><span class="sxs-lookup"><span data-stu-id="29e22-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="29e22-108">有关 NuGet API 实现广泛整个 NuGet 生态系统的信息，请参阅[API 概述](overview.md)。</span><span class="sxs-lookup"><span data-stu-id="29e22-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="29e22-109">本主题列出为各种协议和当到达存在。</span><span class="sxs-lookup"><span data-stu-id="29e22-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="29e22-110">所需的 NuGet 协议版本 4.1.0</span><span class="sxs-lookup"><span data-stu-id="29e22-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="29e22-111">4.1.0 协议指定的作用域验证密钥与除 nuget.org，若要验证针对 nuget.org 帐户之外的服务进行交互的用法。</span><span class="sxs-lookup"><span data-stu-id="29e22-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="29e22-112">请注意，`4.1.0`版本数是不透明的字符串，但不会支持此协议的官方 NuGet 客户端的第一个版本保持一致。</span><span class="sxs-lookup"><span data-stu-id="29e22-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="29e22-113">验证确保用户创建 API 密钥仅用于 nuget.org，并通过一次使用验证范围密钥处理该验证或从第三方服务的验证。</span><span class="sxs-lookup"><span data-stu-id="29e22-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="29e22-114">这些验证范围密钥可以用于验证包属于 nuget.org 上的特定用户 （帐户）。</span><span class="sxs-lookup"><span data-stu-id="29e22-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="29e22-115">客户端要求</span><span class="sxs-lookup"><span data-stu-id="29e22-115">Client requirement</span></span>

<span data-ttu-id="29e22-116">要求客户端传递以下标头，当他们开展 API 调用发布到**推送**nuget.org 的包：</span><span class="sxs-lookup"><span data-stu-id="29e22-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="29e22-117">请注意，`X-NuGet-Client-Version`标头具有相似的语义，但已保留以仅供官方 NuGet 客户端。</span><span class="sxs-lookup"><span data-stu-id="29e22-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="29e22-118">第三方客户端应使用`X-NuGet-Protocol-Version`标头和值。</span><span class="sxs-lookup"><span data-stu-id="29e22-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="29e22-119">**推送**协议本身中的文档所述[`PackagePublish`资源](package-publish-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="29e22-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="29e22-120">如果客户端与外部服务，需要验证是否属于特定用户 （帐户） 的包交互时，它应使用以下协议，并使用作用域的验证密钥和不从 nuget.org 的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="29e22-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="29e22-121">API 来请求作用域的验证密钥</span><span class="sxs-lookup"><span data-stu-id="29e22-121">API to request a verify-scope key</span></span>

<span data-ttu-id="29e22-122">此 API 用于获取 nuget.org 作者，以验证归他/她的包的作用域的验证密钥。</span><span class="sxs-lookup"><span data-stu-id="29e22-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="29e22-123">请求参数</span><span class="sxs-lookup"><span data-stu-id="29e22-123">Request parameters</span></span>

<span data-ttu-id="29e22-124">名称</span><span class="sxs-lookup"><span data-stu-id="29e22-124">Name</span></span>           | <span data-ttu-id="29e22-125">内</span><span class="sxs-lookup"><span data-stu-id="29e22-125">In</span></span>     | <span data-ttu-id="29e22-126">类型</span><span class="sxs-lookup"><span data-stu-id="29e22-126">Type</span></span>   | <span data-ttu-id="29e22-127">必需</span><span class="sxs-lookup"><span data-stu-id="29e22-127">Required</span></span> | <span data-ttu-id="29e22-128">说明</span><span class="sxs-lookup"><span data-stu-id="29e22-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="29e22-129">Id</span><span class="sxs-lookup"><span data-stu-id="29e22-129">ID</span></span>             | <span data-ttu-id="29e22-130">URL</span><span class="sxs-lookup"><span data-stu-id="29e22-130">URL</span></span>    | <span data-ttu-id="29e22-131">字符串</span><span class="sxs-lookup"><span data-stu-id="29e22-131">string</span></span> | <span data-ttu-id="29e22-132">是</span><span class="sxs-lookup"><span data-stu-id="29e22-132">yes</span></span>      | <span data-ttu-id="29e22-133">为其请求验证作用域键包 identidier</span><span class="sxs-lookup"><span data-stu-id="29e22-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="29e22-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="29e22-134">VERSION</span></span>        | <span data-ttu-id="29e22-135">URL</span><span class="sxs-lookup"><span data-stu-id="29e22-135">URL</span></span>    | <span data-ttu-id="29e22-136">字符串</span><span class="sxs-lookup"><span data-stu-id="29e22-136">string</span></span> | <span data-ttu-id="29e22-137">否</span><span class="sxs-lookup"><span data-stu-id="29e22-137">no</span></span>       | <span data-ttu-id="29e22-138">包版本</span><span class="sxs-lookup"><span data-stu-id="29e22-138">The package version</span></span>
<span data-ttu-id="29e22-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="29e22-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="29e22-140">Header</span><span class="sxs-lookup"><span data-stu-id="29e22-140">Header</span></span> | <span data-ttu-id="29e22-141">字符串</span><span class="sxs-lookup"><span data-stu-id="29e22-141">string</span></span> | <span data-ttu-id="29e22-142">是</span><span class="sxs-lookup"><span data-stu-id="29e22-142">yes</span></span>      | <span data-ttu-id="29e22-143">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="29e22-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="29e22-144">响应</span><span class="sxs-lookup"><span data-stu-id="29e22-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="29e22-145">若要验证验证作用域键的 API</span><span class="sxs-lookup"><span data-stu-id="29e22-145">API to verify the verify scope key</span></span>

<span data-ttu-id="29e22-146">此 API 用于验证包归 nuget.org 作者作用域的验证密钥。</span><span class="sxs-lookup"><span data-stu-id="29e22-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="29e22-147">请求参数</span><span class="sxs-lookup"><span data-stu-id="29e22-147">Request parameters</span></span>

<span data-ttu-id="29e22-148">名称</span><span class="sxs-lookup"><span data-stu-id="29e22-148">Name</span></span>           | <span data-ttu-id="29e22-149">内</span><span class="sxs-lookup"><span data-stu-id="29e22-149">In</span></span>     | <span data-ttu-id="29e22-150">类型</span><span class="sxs-lookup"><span data-stu-id="29e22-150">Type</span></span>   | <span data-ttu-id="29e22-151">必需</span><span class="sxs-lookup"><span data-stu-id="29e22-151">Required</span></span> | <span data-ttu-id="29e22-152">说明</span><span class="sxs-lookup"><span data-stu-id="29e22-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="29e22-153">Id</span><span class="sxs-lookup"><span data-stu-id="29e22-153">ID</span></span>             | <span data-ttu-id="29e22-154">URL</span><span class="sxs-lookup"><span data-stu-id="29e22-154">URL</span></span>    | <span data-ttu-id="29e22-155">字符串</span><span class="sxs-lookup"><span data-stu-id="29e22-155">string</span></span> | <span data-ttu-id="29e22-156">是</span><span class="sxs-lookup"><span data-stu-id="29e22-156">yes</span></span>      | <span data-ttu-id="29e22-157">为其请求验证作用域键包标识符</span><span class="sxs-lookup"><span data-stu-id="29e22-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="29e22-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="29e22-158">VERSION</span></span>        | <span data-ttu-id="29e22-159">URL</span><span class="sxs-lookup"><span data-stu-id="29e22-159">URL</span></span>    | <span data-ttu-id="29e22-160">字符串</span><span class="sxs-lookup"><span data-stu-id="29e22-160">string</span></span> | <span data-ttu-id="29e22-161">否</span><span class="sxs-lookup"><span data-stu-id="29e22-161">no</span></span>       | <span data-ttu-id="29e22-162">包版本</span><span class="sxs-lookup"><span data-stu-id="29e22-162">The package version</span></span>
<span data-ttu-id="29e22-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="29e22-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="29e22-164">Header</span><span class="sxs-lookup"><span data-stu-id="29e22-164">Header</span></span> | <span data-ttu-id="29e22-165">字符串</span><span class="sxs-lookup"><span data-stu-id="29e22-165">string</span></span> | <span data-ttu-id="29e22-166">是</span><span class="sxs-lookup"><span data-stu-id="29e22-166">yes</span></span>      | <span data-ttu-id="29e22-167">例如，`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="29e22-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="29e22-168">此验证作用域 API 密钥将在一天的时间之后过期或首次使用，无论哪个操作发生第一次。</span><span class="sxs-lookup"><span data-stu-id="29e22-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="29e22-169">响应</span><span class="sxs-lookup"><span data-stu-id="29e22-169">Response</span></span>

<span data-ttu-id="29e22-170">状态代码</span><span class="sxs-lookup"><span data-stu-id="29e22-170">Status Code</span></span> | <span data-ttu-id="29e22-171">含义</span><span class="sxs-lookup"><span data-stu-id="29e22-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="29e22-172">200</span><span class="sxs-lookup"><span data-stu-id="29e22-172">200</span></span>         | <span data-ttu-id="29e22-173">API 密钥是有效</span><span class="sxs-lookup"><span data-stu-id="29e22-173">The API key is valid</span></span>
<span data-ttu-id="29e22-174">403</span><span class="sxs-lookup"><span data-stu-id="29e22-174">403</span></span>         | <span data-ttu-id="29e22-175">API 密钥是无效或未授权推送对包</span><span class="sxs-lookup"><span data-stu-id="29e22-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="29e22-176">404</span><span class="sxs-lookup"><span data-stu-id="29e22-176">404</span></span>         | <span data-ttu-id="29e22-177">引用包`ID`和`VERSION`（可选） 不存在</span><span class="sxs-lookup"><span data-stu-id="29e22-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>