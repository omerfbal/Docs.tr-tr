---
title: "ASP.NET Core kaynak tabanlı yetkilendirme"
author: scottaddie
description: "Bir Authorize özniteliği yeterli olmaz, bir ASP.NET Core uygulamada kaynak tabanlı bir yetkilendirme uygulamak öğrenin."
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 11/07/2017
ms.devlang: csharp
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/resourcebased
ms.openlocfilehash: 708f306da740870b106cbeeb96879480f8745439
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/10/2017
---
# <a name="resource-based-authorization"></a><span data-ttu-id="6c9d7-103">Kaynak tabanlı bir yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="6c9d7-103">Resource-based authorization</span></span>

<span data-ttu-id="6c9d7-104">Tarafından [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="6c9d7-104">By [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="6c9d7-105">Yetkilendirme stratejisi erişilen kaynak bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-105">Authorization strategy depends upon the resource being accessed.</span></span> <span data-ttu-id="6c9d7-106">Bir yazar özelliği olan bir belgeyi göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-106">Consider a document which has an author property.</span></span> <span data-ttu-id="6c9d7-107">Yalnızca yazarın belge güncelleştirme izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-107">Only the author is allowed to update the document.</span></span> <span data-ttu-id="6c9d7-108">Sonuç olarak, yetkilendirme değerlendirme oluşabilmesi için öncelikle belge veri deposundan alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-108">Consequently, the document must be retrieved from the data store before authorization evaluation can occur.</span></span>

<span data-ttu-id="6c9d7-109">Veri bağlama ve sayfa işleyici veya belge yükleyen eylem yürütülmesi önce öznitelik değerlendirme oluşur.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-109">Attribute evaluation occurs before data binding and before execution of the page handler or action which loads the document.</span></span> <span data-ttu-id="6c9d7-110">Bu nedenlerle, bildirim temelli yetkilendirme ile bir `[Authorize]` özniteliği yeterli olmaz.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-110">For these reasons, declarative authorization with an `[Authorize]` attribute won't suffice.</span></span> <span data-ttu-id="6c9d7-111">Bunun yerine, bir özel yetkilendirme yöntemi çağırabilirsiniz&mdash;kesinlik temelli yetkilendirme olarak bilinen bir stili.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-111">Instead, you can invoke a custom authorization method&mdash;a style known as imperative authorization.</span></span>

<span data-ttu-id="6c9d7-112">Kullanım [örnek uygulamaları](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/resourcebased/samples) ([nasıl indirileceğini](xref:tutorials/index#how-to-download-a-sample)) Bu konuda açıklanan özellikleri keşfetmek için.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-112">Use the [sample apps](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/resourcebased/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample)) to explore the features described in this topic.</span></span>

## <a name="use-imperative-authorization"></a><span data-ttu-id="6c9d7-113">Kesinlik temelli yetkilendirme kullanın</span><span class="sxs-lookup"><span data-stu-id="6c9d7-113">Use imperative authorization</span></span>

<span data-ttu-id="6c9d7-114">Yetkilendirme olarak gerçekleştirilen bir [IAuthorizationService](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationservice) hizmet ve hizmet koleksiyonu içinde kayıtlı `Startup` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-114">Authorization is implemented as an [IAuthorizationService](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationservice) service and is registered in the service collection within the `Startup` class.</span></span> <span data-ttu-id="6c9d7-115">Hizmet aracılığıyla kullanılabilir hale getirileceğini [bağımlılık ekleme](xref:fundamentals/dependency-injection#fundamentals-dependency-injection) sayfa işleyicileri veya eylemler.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-115">The service is made available via [dependency injection](xref:fundamentals/dependency-injection#fundamentals-dependency-injection) to page handlers or actions.</span></span>

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Controllers/DocumentController.cs?name=snippet_IAuthServiceDI&highlight=6)]

<span data-ttu-id="6c9d7-116">`IAuthorizationService`iki sahip `AuthorizeAsync` yöntemi aşırı: kaynak ve ilke adını ve diğer kaynak ve değerlendirmek için gereksinimlerin listesi kabul bir kabul etme.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-116">`IAuthorizationService` has two `AuthorizeAsync` method overloads: one accepting the resource and the policy name and the other accepting the resource and a list of requirements to evaluate.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="6c9d7-117">ASP.NET 2.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="6c9d7-117">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          IEnumerable<IAuthorizationRequirement> requirements);
Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          string policyName);
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="6c9d7-118">ASP.NET 1.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="6c9d7-118">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
Task<bool> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          IEnumerable<IAuthorizationRequirement> requirements);
Task<bool> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          string policyName);
```

---

<a name="security-authorization-resource-based-imperative"></a>

<span data-ttu-id="6c9d7-119">Aşağıdaki örnekte, güvenli olması için kaynağın özel yüklendi `Document` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-119">In the following example, the resource to be secured is loaded into a custom `Document` object.</span></span> <span data-ttu-id="6c9d7-120">Bir `AuthorizeAsync` aşırı geçerli kullanıcının sağlanan belgeyi düzenlemesine izin verilip verilmediğini belirlemek için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-120">An `AuthorizeAsync` overload is invoked to determine whether the current user is allowed to edit the provided document.</span></span> <span data-ttu-id="6c9d7-121">Özel bir "EditPolicy" yetkilendirme ilkesi karar katılır.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-121">A custom "EditPolicy" authorization policy is factored into the decision.</span></span> <span data-ttu-id="6c9d7-122">Bkz: [özel ilke tabanlı yetkilendirme](xref:security/authorization/policies) yetkilendirme ilkeleri oluşturma hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-122">See [Custom policy-based authorization](xref:security/authorization/policies) for more on creating authorization policies.</span></span>

> [!NOTE]
> <span data-ttu-id="6c9d7-123">Aşağıdaki kod örnekleri varsayın kimlik doğrulaması çalıştıktan ve kümesi `User` özelliği.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-123">The following code samples assume authentication has run and set the `User` property.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="6c9d7-124">ASP.NET 2.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="6c9d7-124">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Pages/Document/Edit.cshtml.cs?name=snippet_DocumentEditHandler)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="6c9d7-125">ASP.NET 1.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="6c9d7-125">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Controllers/DocumentController.cs?name=snippet_DocumentEditAction)]

---

## <a name="write-a-resource-based-handler"></a><span data-ttu-id="6c9d7-126">Kaynak tabanlı işleyicisi yazma</span><span class="sxs-lookup"><span data-stu-id="6c9d7-126">Write a resource-based handler</span></span>

<span data-ttu-id="6c9d7-127">Kaynak tabanlı bir yetkilendirme çok farklı değildir için bir işleyici yazmak [düz gereksinimleri işleyicisi yazma](xref:security/authorization/policies#security-authorization-policies-based-authorization-handler).</span><span class="sxs-lookup"><span data-stu-id="6c9d7-127">Writing a handler for resource-based authorization isn't much different than [writing a plain requirements handler](xref:security/authorization/policies#security-authorization-policies-based-authorization-handler).</span></span> <span data-ttu-id="6c9d7-128">Bir özel gereksinim sınıf oluşturun ve bir gereksinim işleyici sınıf uygulama.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-128">Create a custom requirement class, and implement a requirement handler class.</span></span> <span data-ttu-id="6c9d7-129">İşleyici sınıfını gereksinimi ve kaynak türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-129">The handler class specifies both the requirement and resource type.</span></span> <span data-ttu-id="6c9d7-130">Örneğin, bir işleyici kullanan bir `SameAuthorRequirement` gereksinim ve `Document` kaynak arar:</span><span class="sxs-lookup"><span data-stu-id="6c9d7-130">For example, a handler utilizing a `SameAuthorRequirement` requirement and a `Document` resource looks as follows:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="6c9d7-131">ASP.NET 2.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="6c9d7-131">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationHandler.cs?name=snippet_HandlerAndRequirement)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="6c9d7-132">ASP.NET 1.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="6c9d7-132">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Services/DocumentAuthorizationHandler.cs?name=snippet_HandlerAndRequirement)]

---

<span data-ttu-id="6c9d7-133">Gereksinim ve işleyicisinde kaydetmek `Startup.ConfigureServices` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="6c9d7-133">Register the requirement and handler in the `Startup.ConfigureServices` method:</span></span>

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Startup.cs?name=snippet_ConfigureServicesSample&highlight=3-7,9)]

### <a name="operational-requirements"></a><span data-ttu-id="6c9d7-134">İşletimsel gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="6c9d7-134">Operational requirements</span></span>

<span data-ttu-id="6c9d7-135">CRUD sonuçları temel alarak kararları yapıyorsanız, (**C**oluştur, **R**okunur, **U**pdate'i, **D**Sil) işlemleri, kullanın [OperationAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.infrastructure.operationauthorizationrequirement) yardımcı sınıfı.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-135">If you're making decisions based on the outcomes of CRUD (**C**reate, **R**ead, **U**pdate, **D**elete) operations, use the [OperationAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.infrastructure.operationauthorizationrequirement) helper class.</span></span> <span data-ttu-id="6c9d7-136">Bu sınıf, her işlem türü için ayrı bir sınıf yerine tek bir işleyici yazmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-136">This class enables you to write a single handler instead of an individual class for each operation type.</span></span> <span data-ttu-id="6c9d7-137">Kullanmak için bazı işlem adları sağlayın:</span><span class="sxs-lookup"><span data-stu-id="6c9d7-137">To use it, provide some operation names:</span></span>

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_OperationsClass)]

<span data-ttu-id="6c9d7-138">İşleyici kullanılarak aşağıdaki gibi uygulanan bir `OperationAuthorizationRequirement` gereksinim ve `Document` kaynak:</span><span class="sxs-lookup"><span data-stu-id="6c9d7-138">The handler is implemented as follows, using an `OperationAuthorizationRequirement` requirement and a `Document` resource:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="6c9d7-139">ASP.NET 2.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="6c9d7-139">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_Handler)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="6c9d7-140">ASP.NET 1.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="6c9d7-140">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_Handler)]

---

<span data-ttu-id="6c9d7-141">Kaynak, kullanıcının kimliğini ve gereksinimi 's kullanarak işlemi önceki işleyici doğrular `Name` özelliği.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-141">The preceding handler validates the operation using the resource, the user's identity, and the requirement's `Name` property.</span></span>

<span data-ttu-id="6c9d7-142">Bir işlem kaynak işleyicisi çağırmak için işlem çağrılırken, belirtin `AuthorizeAsync` sayfası işleyicisi veya eylem.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-142">To call an operational resource handler, specify the operation when invoking `AuthorizeAsync` in your page handler or action.</span></span> <span data-ttu-id="6c9d7-143">Aşağıdaki örnek, kimliği doğrulanmış kullanıcının sağlanan belgeyi görüntülemek için izin verilip verilmediğini belirler.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-143">The following example determines whether the authenticated user is permitted to view the provided document.</span></span>

> [!NOTE]
> <span data-ttu-id="6c9d7-144">Aşağıdaki kod örnekleri varsayın kimlik doğrulaması çalıştıktan ve kümesi `User` özelliği.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-144">The following code samples assume authentication has run and set the `User` property.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="6c9d7-145">ASP.NET 2.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="6c9d7-145">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Pages/Document/View.cshtml.cs?name=snippet_DocumentViewHandler&highlight=10-11)]

<span data-ttu-id="6c9d7-146">Yetkilendirme başarılı olursa, belgeyi görüntülemek için sayfanın döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-146">If authorization succeeds, the page for viewing the document is returned.</span></span> <span data-ttu-id="6c9d7-147">Yetkilendirme başarısız olur, ancak kullanıcının kimliği doğrulanır varsa, döndürme `ForbidResult` yetkilendirme başarısız oldu herhangi bir kimlik doğrulaması ara yazılımı bildirir.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-147">If authorization fails but the user is authenticated, returning `ForbidResult` informs any authentication middleware that authorization failed.</span></span> <span data-ttu-id="6c9d7-148">A `ChallengeResult` kimlik doğrulaması gerçekleştirilmesi gereken döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-148">A `ChallengeResult` is returned when authentication must be performed.</span></span> <span data-ttu-id="6c9d7-149">Etkileşimli tarayıcı istemcileri için kullanıcının oturum açma sayfasına yeniden yönlendirmek uygun olabilir.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-149">For interactive browser clients, it may be appropriate to redirect the user to a login page.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="6c9d7-150">ASP.NET 1.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="6c9d7-150">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Controllers/DocumentController.cs?name=snippet_DocumentViewAction&highlight=11-12)]

<span data-ttu-id="6c9d7-151">Yetkilendirme başarılı olursa, belge için görünümü döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-151">If authorization succeeds, the view for the document is returned.</span></span> <span data-ttu-id="6c9d7-152">Yetkilendirme başarısız olursa, döndürme `ChallengeResult` herhangi bir kimlik doğrulaması ara yazılımı yetkilendirme başarısız oldu ve ara yazılım uygun yanıtı alabilir bildirir.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-152">If authorization fails, returning `ChallengeResult` informs any authentication middleware that authorization failed, and the middleware can take the appropriate response.</span></span> <span data-ttu-id="6c9d7-153">Uygun bir yanıt bir 401 veya 403 durum kodu döndürüyor.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-153">An appropriate response could be returning a 401 or 403 status code.</span></span> <span data-ttu-id="6c9d7-154">Etkileşimli tarayıcı istemcileri için kullanıcı bir oturum açma sayfasına yeniden yönlendirmeye anlamına gelebilir.</span><span class="sxs-lookup"><span data-stu-id="6c9d7-154">For interactive browser clients, it could mean redirecting the user to a login page.</span></span>

---