---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: "ASP.NET Web API 2 yapılandırma | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2014
ms.topic: article
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 1c007c4c327b7cde6ff52c6b0022acdff3c9b137
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/10/2017
---
<a name="configuring-aspnet-web-api-2"></a><span data-ttu-id="164d3-102">ASP.NET Web API 2 yapılandırma</span><span class="sxs-lookup"><span data-stu-id="164d3-102">Configuring ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="164d3-103">tarafından [CAN Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="164d3-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="164d3-104">Bu konu, ASP.NET Web API yapılandırmasını açıklar.</span><span class="sxs-lookup"><span data-stu-id="164d3-104">This topic describes how to configure ASP.NET Web API.</span></span>

- [<span data-ttu-id="164d3-105">Yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="164d3-105">Configuration Settings</span></span>](#settings)
- [<span data-ttu-id="164d3-106">ASP.NET barındırma ile Web API yapılandırma</span><span class="sxs-lookup"><span data-stu-id="164d3-106">Configuring Web API with ASP.NET Hosting</span></span>](#webhost)
- [<span data-ttu-id="164d3-107">Web API OWIN kendi kendine barındırma ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="164d3-107">Configuring Web API with OWIN Self-Hosting</span></span>](#selfhost)
- [<span data-ttu-id="164d3-108">Genel Web API Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="164d3-108">Global Web API Services</span></span>](#services)
- [<span data-ttu-id="164d3-109">Denetleyici başına yapılandırma</span><span class="sxs-lookup"><span data-stu-id="164d3-109">Per-Controller Configuration</span></span>](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a><span data-ttu-id="164d3-110">Yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="164d3-110">Configuration Settings</span></span>

<span data-ttu-id="164d3-111">Web API yapılandırması ayarları tanımlanmış [HttpConfiguration](https://msdn.microsoft.com/en-us/library/system.web.http.httpconfiguration.aspx) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="164d3-111">Web API configuration setttings are defined in the [HttpConfiguration](https://msdn.microsoft.com/en-us/library/system.web.http.httpconfiguration.aspx) class.</span></span>

| <span data-ttu-id="164d3-112">Üye</span><span class="sxs-lookup"><span data-stu-id="164d3-112">Member</span></span> | <span data-ttu-id="164d3-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="164d3-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="164d3-114">**DependencyResolver**</span><span class="sxs-lookup"><span data-stu-id="164d3-114">**DependencyResolver**</span></span> | <span data-ttu-id="164d3-115">Bağımlılık ekleme denetleyicileri için etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="164d3-115">Enables dependency injection for controllers.</span></span> <span data-ttu-id="164d3-116">Bkz: [Web API bağımlılık çözümleyicisini kullanarak](dependency-injection.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-116">See [Using the Web API Dependency Resolver](dependency-injection.md).</span></span> |
| <span data-ttu-id="164d3-117">**Filtreleri**</span><span class="sxs-lookup"><span data-stu-id="164d3-117">**Filters**</span></span> | <span data-ttu-id="164d3-118">Eylem filtreleri.</span><span class="sxs-lookup"><span data-stu-id="164d3-118">Action filters.</span></span> |
| <span data-ttu-id="164d3-119">**Biçimlendiricileri**</span><span class="sxs-lookup"><span data-stu-id="164d3-119">**Formatters**</span></span> | <span data-ttu-id="164d3-120">[Medya türü biçimlendiricilerini](../formats-and-model-binding/media-formatters.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-120">[Media-type formatters](../formats-and-model-binding/media-formatters.md).</span></span> |
| <span data-ttu-id="164d3-121">**IncludeErrorDetailPolicy**</span><span class="sxs-lookup"><span data-stu-id="164d3-121">**IncludeErrorDetailPolicy**</span></span> | <span data-ttu-id="164d3-122">Sunucu özel durum iletileri ve Yığın izlemeleri gibi hata ayrıntılarının HTTP yanıt iletilerini dahil olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="164d3-122">Specifies whether the server should include error details, such as exception messages and stack traces, in HTTP response messages.</span></span> <span data-ttu-id="164d3-123">Bkz: [IncludeErrorDetailPolicy](https://msdn.microsoft.com/en-us/library/system.web.http.includeerrordetailpolicy(v=vs.108)).</span><span class="sxs-lookup"><span data-stu-id="164d3-123">See [IncludeErrorDetailPolicy](https://msdn.microsoft.com/en-us/library/system.web.http.includeerrordetailpolicy(v=vs.108)).</span></span> |
| <span data-ttu-id="164d3-124">**Başlatıcı**</span><span class="sxs-lookup"><span data-stu-id="164d3-124">**Initializer**</span></span> | <span data-ttu-id="164d3-125">Öğesinin son başlatılmasını gerçekleştiren bir işlev **HttpConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="164d3-125">A function that performs final initialization of the **HttpConfiguration**.</span></span> |
| <span data-ttu-id="164d3-126">**MessageHandlers**</span><span class="sxs-lookup"><span data-stu-id="164d3-126">**MessageHandlers**</span></span> | <span data-ttu-id="164d3-127">[HTTP ileti işleyicileri](http-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-127">[HTTP message handlers](http-message-handlers.md).</span></span> |
| <span data-ttu-id="164d3-128">**ParameterBindingRules**</span><span class="sxs-lookup"><span data-stu-id="164d3-128">**ParameterBindingRules**</span></span> | <span data-ttu-id="164d3-129">Denetleyici eylemleri parametre bağlama için kurallar topluluğu.</span><span class="sxs-lookup"><span data-stu-id="164d3-129">A collection of rules for binding parameters on controller actions.</span></span> |
| <span data-ttu-id="164d3-130">**Veri Erişimi**</span><span class="sxs-lookup"><span data-stu-id="164d3-130">**Properties**</span></span> | <span data-ttu-id="164d3-131">Genel özellik paketi.</span><span class="sxs-lookup"><span data-stu-id="164d3-131">A generic property bag.</span></span> |
| <span data-ttu-id="164d3-132">**Rotalar**</span><span class="sxs-lookup"><span data-stu-id="164d3-132">**Routes**</span></span> | <span data-ttu-id="164d3-133">Rota koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="164d3-133">The collection of routes.</span></span> <span data-ttu-id="164d3-134">Bkz: [ASP.NET Web API'de yönlendirme](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-134">See [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="164d3-135">**Hizmetleri**</span><span class="sxs-lookup"><span data-stu-id="164d3-135">**Services**</span></span> | <span data-ttu-id="164d3-136">Hizmetler koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="164d3-136">The collection of services.</span></span> <span data-ttu-id="164d3-137">Bkz: [Hizmetleri](#services).</span><span class="sxs-lookup"><span data-stu-id="164d3-137">See [Services](#services).</span></span> |


## <a name="prerequisites"></a><span data-ttu-id="164d3-138">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="164d3-138">Prerequisites</span></span>

<span data-ttu-id="164d3-139">[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional veya Enterprise sürümü.</span><span class="sxs-lookup"><span data-stu-id="164d3-139">[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional, or Enterprise Edition.</span></span>

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a><span data-ttu-id="164d3-140">ASP.NET barındırma ile Web API yapılandırma</span><span class="sxs-lookup"><span data-stu-id="164d3-140">Configuring Web API with ASP.NET Hosting</span></span>

<span data-ttu-id="164d3-141">Bir ASP.NET uygulamasındaki Web API'sini çağırarak yapılandırma [GlobalConfiguration.Configure](https://msdn.microsoft.com/en-us/library/system.web.http.globalconfiguration.configure.aspx) içinde **uygulama\_Başlat** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="164d3-141">In an ASP.NET application, configure Web API by calling [GlobalConfiguration.Configure](https://msdn.microsoft.com/en-us/library/system.web.http.globalconfiguration.configure.aspx) in the **Application\_Start** method.</span></span> <span data-ttu-id="164d3-142">**Yapılandırma** yöntemi alır bir temsilci türü tek bir parametre ile **HttpConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="164d3-142">The **Configure** method takes a delegate with a single parameter of type **HttpConfiguration**.</span></span> <span data-ttu-id="164d3-143">Tüm temsilci içinde geçiyor gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="164d3-143">Perform all of your configuation inside the delegate.</span></span>

<span data-ttu-id="164d3-144">Anonim bir temsilci kullanarak örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="164d3-144">Here is an example using an anonymous delegate:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="164d3-145">"Web API'sini"'yı seçerseniz Visual Studio 2017, "ASP.NET Web uygulaması" proje şablonu yapılandırma kodu, otomatik olarak ayarlar. **yeni ASP.NET projesi** iletişim.</span><span class="sxs-lookup"><span data-stu-id="164d3-145">In Visual Studio 2017, the "ASP.NET Web Application" project template automatically sets up the configuration code, if you select "Web API" in the **New ASP.NET Project** dialog.</span></span>

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

<span data-ttu-id="164d3-146">Proje şablonu uygulama içinde WebApiConfig.cs adlı bir dosya oluşturur\_başlangıç klasörü.</span><span class="sxs-lookup"><span data-stu-id="164d3-146">The project template creates a file named WebApiConfig.cs inside the App\_Start folder.</span></span> <span data-ttu-id="164d3-147">Bu kod dosyası, Web API yapılandırması kodunuzu nereye yerleştirileceği temsilci tanımlar.</span><span class="sxs-lookup"><span data-stu-id="164d3-147">This code file defines the delegate where you should put your Web API configuration code.</span></span>

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

<span data-ttu-id="164d3-148">Proje şablonu de temsilciden çağıran kodu ekler **uygulama\_Başlat**.</span><span class="sxs-lookup"><span data-stu-id="164d3-148">The project template also adds the code that calls the delegate from **Application\_Start**.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a><span data-ttu-id="164d3-149">Web API OWIN kendi kendine barındırma ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="164d3-149">Configuring Web API with OWIN Self-Hosting</span></span>

<span data-ttu-id="164d3-150">OWIN ile kendi kendine barındırma varsa, yeni bir oluşturma **HttpConfiguration** örneği.</span><span class="sxs-lookup"><span data-stu-id="164d3-150">If you are self-hosting with OWIN, create a new **HttpConfiguration** instance.</span></span> <span data-ttu-id="164d3-151">Bu örneği üzerinde herhangi bir yapılandırma gerçekleştirebilir ve örneğine geçirmek **Owin.UseWebApi** genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="164d3-151">Perform any configuration on this instance, and then pass the instance to the **Owin.UseWebApi** extension method.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="164d3-152">Öğretici [Self-Host ASP.NET Web API 2 kullanım OWIN](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) tam adımlar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="164d3-152">The tutorial [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) shows the complete steps.</span></span>

<a id="services"></a>
## <a name="global-web-api-services"></a><span data-ttu-id="164d3-153">Genel Web API Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="164d3-153">Global Web API Services</span></span>

<span data-ttu-id="164d3-154">**HttpConfiguration.Services** koleksiyonu, bir Web API denetleyicisi seçimi ve içerik anlaşması gibi çeşitli görevleri gerçekleştirmek için kullandığı genel hizmetler kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="164d3-154">The **HttpConfiguration.Services** collection contains a set of global services that Web API uses to perform various tasks, such as controller selection and content negotiation.</span></span>

> [!NOTE]
> <span data-ttu-id="164d3-155">**Hizmetleri** koleksiyonu hizmet bulma veya bağımlılık ekleme işlemi için genel amaçlı bir mekanizma değil.</span><span class="sxs-lookup"><span data-stu-id="164d3-155">The **Services** collection is not a general-purpose mechanism for service discovery or dependency injection.</span></span> <span data-ttu-id="164d3-156">Yalnızca Web API çerçevesi bilinen hizmet türleri de depolar.</span><span class="sxs-lookup"><span data-stu-id="164d3-156">It only stores service types that are known to the Web API framework.</span></span>


<span data-ttu-id="164d3-157">**Hizmetleri** koleksiyonu Hizmetleri varsayılan kümesiyle başlatılır ve kendi özel uygulamalar sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="164d3-157">The **Services** collection is initialized with a default set of services, and you can provide your own custom implementations.</span></span> <span data-ttu-id="164d3-158">Başkalarının yalnızca bir örneği olabilir ancak bazı hizmetler birden çok örneği destekler.</span><span class="sxs-lookup"><span data-stu-id="164d3-158">Some services support multiple instances, while others can have only one instance.</span></span> <span data-ttu-id="164d3-159">(Ancak, hizmetleri denetleyici düzeyinde de sağlayabilirsiniz; bkz [denetleyicisi başına yapılandırma](#percontrollerconfig).</span><span class="sxs-lookup"><span data-stu-id="164d3-159">(However, you can also provide services at the controller level; see [Per-Controller Configuration](#percontrollerconfig).</span></span>

<span data-ttu-id="164d3-160">Tek Örnekli Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="164d3-160">Single-Instance Services</span></span>


| <span data-ttu-id="164d3-161">Hizmet</span><span class="sxs-lookup"><span data-stu-id="164d3-161">Service</span></span> | <span data-ttu-id="164d3-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="164d3-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="164d3-163">**IActionValueBinder**</span><span class="sxs-lookup"><span data-stu-id="164d3-163">**IActionValueBinder**</span></span> | <span data-ttu-id="164d3-164">Bir parametre için bir bağlama alır.</span><span class="sxs-lookup"><span data-stu-id="164d3-164">Gets a binding for a parameter.</span></span> |
| <span data-ttu-id="164d3-165">**IApiExplorer**</span><span class="sxs-lookup"><span data-stu-id="164d3-165">**IApiExplorer**</span></span> | <span data-ttu-id="164d3-166">Uygulama tarafından sunulan API'lerde açıklamalarını alır.</span><span class="sxs-lookup"><span data-stu-id="164d3-166">Gets descriptions of the APIs exposed by the application.</span></span> <span data-ttu-id="164d3-167">Bkz: [Web API'si için bir Yardım sayfası oluşturma](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-167">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="164d3-168">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="164d3-168">**IAssembliesResolver**</span></span> | <span data-ttu-id="164d3-169">Uygulama için bir derleme listesi alır.</span><span class="sxs-lookup"><span data-stu-id="164d3-169">Gets a list of the assemblies for the application.</span></span> <span data-ttu-id="164d3-170">Bkz: [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-170">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="164d3-171">**IBodyModelValidator**</span><span class="sxs-lookup"><span data-stu-id="164d3-171">**IBodyModelValidator**</span></span> | <span data-ttu-id="164d3-172">İstek gövdesinden medya türü biçimlendirici tarafından okunur modeli doğrular.</span><span class="sxs-lookup"><span data-stu-id="164d3-172">Validates a model that is read from the request body by a media-type formatter.</span></span> |
| <span data-ttu-id="164d3-173">**IContentNegotiator**</span><span class="sxs-lookup"><span data-stu-id="164d3-173">**IContentNegotiator**</span></span> | <span data-ttu-id="164d3-174">İçerik anlaşması gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="164d3-174">Performs content negotiation.</span></span> |
| <span data-ttu-id="164d3-175">**IDocumentationProvider**</span><span class="sxs-lookup"><span data-stu-id="164d3-175">**IDocumentationProvider**</span></span> | <span data-ttu-id="164d3-176">API için belgeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="164d3-176">Provides documentation for APIs.</span></span> <span data-ttu-id="164d3-177">Varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="164d3-177">The default is **null**.</span></span> <span data-ttu-id="164d3-178">Bkz: [Web API'si için bir Yardım sayfası oluşturma](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-178">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="164d3-179">**IHostBufferPolicySelector**</span><span class="sxs-lookup"><span data-stu-id="164d3-179">**IHostBufferPolicySelector**</span></span> | <span data-ttu-id="164d3-180">Ana HTTP ileti varlık gövdeleri arabelleğe alıp almayacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="164d3-180">Indicates whether the host should buffer HTTP message entity bodies.</span></span> |
| <span data-ttu-id="164d3-181">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="164d3-181">**IHttpActionInvoker**</span></span> | <span data-ttu-id="164d3-182">Bir denetleyici eylemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="164d3-182">Invokes a controller action.</span></span> <span data-ttu-id="164d3-183">Bkz: [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-183">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="164d3-184">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="164d3-184">**IHttpActionSelector**</span></span> | <span data-ttu-id="164d3-185">Bir denetleyici eylemi seçer.</span><span class="sxs-lookup"><span data-stu-id="164d3-185">Selects a controller action.</span></span> <span data-ttu-id="164d3-186">Bkz: [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-186">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="164d3-187">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="164d3-187">**IHttpControllerActivator**</span></span> | <span data-ttu-id="164d3-188">Bir denetleyici etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="164d3-188">Activates a controller.</span></span> <span data-ttu-id="164d3-189">Bkz: [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-189">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="164d3-190">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="164d3-190">**IHttpControllerSelector**</span></span> | <span data-ttu-id="164d3-191">Bir denetleyiciyi seçer.</span><span class="sxs-lookup"><span data-stu-id="164d3-191">Selects a controller.</span></span> <span data-ttu-id="164d3-192">Bkz: [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-192">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="164d3-193">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="164d3-193">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="164d3-194">Uygulamadaki Web API denetleyicisi türlerinin bir listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="164d3-194">Provides a list of the Web API controller types in the application.</span></span> <span data-ttu-id="164d3-195">Bkz: [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-195">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="164d3-196">**ITraceManager**</span><span class="sxs-lookup"><span data-stu-id="164d3-196">**ITraceManager**</span></span> | <span data-ttu-id="164d3-197">İzleme çerçevesini başlatır.</span><span class="sxs-lookup"><span data-stu-id="164d3-197">Initializes the tracing framework.</span></span> <span data-ttu-id="164d3-198">Bkz: [ASP.NET Web API izleme](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-198">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="164d3-199">**ITraceWriter**</span><span class="sxs-lookup"><span data-stu-id="164d3-199">**ITraceWriter**</span></span> | <span data-ttu-id="164d3-200">İzleme yazıcısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="164d3-200">Provides a trace writer.</span></span> <span data-ttu-id="164d3-201">"No-op" izleme yazıcısı varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="164d3-201">The default is a "no-op" trace writer.</span></span> <span data-ttu-id="164d3-202">Bkz: [ASP.NET Web API izleme](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="164d3-202">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="164d3-203">**IModelValidatorCache**</span><span class="sxs-lookup"><span data-stu-id="164d3-203">**IModelValidatorCache**</span></span> | <span data-ttu-id="164d3-204">Model doğrulayıcılarının oluşan bir önbellek sağlar.</span><span class="sxs-lookup"><span data-stu-id="164d3-204">Provides a cache of model validators.</span></span> |

<span data-ttu-id="164d3-205">Birden çok örnekli Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="164d3-205">Multiple-Instance Services</span></span>


| <span data-ttu-id="164d3-206">Hizmet</span><span class="sxs-lookup"><span data-stu-id="164d3-206">Service</span></span> | <span data-ttu-id="164d3-207">Açıklama</span><span class="sxs-lookup"><span data-stu-id="164d3-207">Description</span></span> |
| --- | --- |
| <span data-ttu-id="164d3-208">**IFilterProvider**</span><span class="sxs-lookup"><span data-stu-id="164d3-208">**IFilterProvider**</span></span> | <span data-ttu-id="164d3-209">Bir denetleyici eylemi için filtreleri listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="164d3-209">Returns a list of filters for a controller action.</span></span> |
| <span data-ttu-id="164d3-210">**ModelBinderProvider**</span><span class="sxs-lookup"><span data-stu-id="164d3-210">**ModelBinderProvider**</span></span> | <span data-ttu-id="164d3-211">Belirtilen tür için model bağlayıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="164d3-211">Returns a model binder for a given type.</span></span> |
| <span data-ttu-id="164d3-212">**ModelMetadataProvider**</span><span class="sxs-lookup"><span data-stu-id="164d3-212">**ModelMetadataProvider**</span></span> | <span data-ttu-id="164d3-213">Bir model için meta veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="164d3-213">Provides metadata for a model.</span></span> |
| <span data-ttu-id="164d3-214">**ModelValidatorProvider**</span><span class="sxs-lookup"><span data-stu-id="164d3-214">**ModelValidatorProvider**</span></span> | <span data-ttu-id="164d3-215">Bir model için bir doğrulayıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="164d3-215">Provides a validator for a model.</span></span> |
| <span data-ttu-id="164d3-216">**ValueProviderFactory**</span><span class="sxs-lookup"><span data-stu-id="164d3-216">**ValueProviderFactory**</span></span> | <span data-ttu-id="164d3-217">Bir değer sağlayıcısı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="164d3-217">Creates a value provider.</span></span> <span data-ttu-id="164d3-218">Daha fazla bilgi için bkz: CAN kabini'nın blog gönderisi [Webapı içinde bir özel değer sağlayıcı oluşturma](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span><span class="sxs-lookup"><span data-stu-id="164d3-218">For more information, see Mike Stall's blog post [How to create a custom value provider in WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span></span> |<span data-ttu-id="164d3-219">biçimindeki telefon numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="164d3-219">.</span></span>

<span data-ttu-id="164d3-220">Çok örnekli bir hizmetin özel bir uygulama eklemek için arama **Ekle** veya **Ekle** üzerinde **Hizmetleri** koleksiyonu:</span><span class="sxs-lookup"><span data-stu-id="164d3-220">To add a custom implementation to a multi-instance service, call **Add** or **Insert** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="164d3-221">Tek Örnekli bir hizmeti özel bir uygulama ile değiştirmek için arama **Değiştir** üzerinde **Hizmetleri** koleksiyonu:</span><span class="sxs-lookup"><span data-stu-id="164d3-221">To replace a single-instance service with a custom implementation, call **Replace** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a><span data-ttu-id="164d3-222">Denetleyici başına yapılandırma</span><span class="sxs-lookup"><span data-stu-id="164d3-222">Per-Controller Configuration</span></span>

<span data-ttu-id="164d3-223">Denetleyici başına temelinde aşağıdaki ayarları geçersiz kılabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="164d3-223">You can override the following settings on a per-controller basis:</span></span>

- <span data-ttu-id="164d3-224">Medya türü biçimlendiricileri</span><span class="sxs-lookup"><span data-stu-id="164d3-224">Media-type formatters</span></span>
- <span data-ttu-id="164d3-225">Parametre bağlama kuralları</span><span class="sxs-lookup"><span data-stu-id="164d3-225">Parameter binding rules</span></span>
- <span data-ttu-id="164d3-226">Hizmetler</span><span class="sxs-lookup"><span data-stu-id="164d3-226">Services</span></span>

<span data-ttu-id="164d3-227">Bunu yapmak için uygulayan özel bir öznitelik tanımlamak **IControllerConfiguration** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="164d3-227">To do so, define a custom attribute that implements the **IControllerConfiguration** interface.</span></span> <span data-ttu-id="164d3-228">Ardından özniteliği denetleyiciye uygulanır.</span><span class="sxs-lookup"><span data-stu-id="164d3-228">Then apply the attribute to the controller.</span></span>

<span data-ttu-id="164d3-229">Aşağıdaki örnek ile özel bir Biçimlendiricinin varsayılan medya türü biçimlendiricilerini yerini alır.</span><span class="sxs-lookup"><span data-stu-id="164d3-229">The following example replaces the default media-type formatters with a custom formatter.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="164d3-230">**IControllerConfiguration.Initialize** yöntemi iki parametre alır:</span><span class="sxs-lookup"><span data-stu-id="164d3-230">The **IControllerConfiguration.Initialize** method takes two parameters:</span></span>

- <span data-ttu-id="164d3-231">Bir **HttpControllerSettings** nesnesi</span><span class="sxs-lookup"><span data-stu-id="164d3-231">An **HttpControllerSettings** object</span></span>
- <span data-ttu-id="164d3-232">Bir **HttpControllerDescriptor** nesnesi</span><span class="sxs-lookup"><span data-stu-id="164d3-232">An **HttpControllerDescriptor** object</span></span>

<span data-ttu-id="164d3-233">**HttpControllerDescriptor** (iki denetleyicileri arasında ayrım yapmak için say,) bilgilendirme amacıyla inceleyebilirsiniz denetleyicisi açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="164d3-233">The **HttpControllerDescriptor** contains a description of the controller, which you can examine for informational purposes (say, to distinguish between two controllers).</span></span>

<span data-ttu-id="164d3-234">Kullanım **HttpControllerSettings** denetleyicisi yapılandırmak için nesne.</span><span class="sxs-lookup"><span data-stu-id="164d3-234">Use the **HttpControllerSettings** object to configure the controller.</span></span> <span data-ttu-id="164d3-235">Bu nesne alt bir denetleyici başına temelinde kılabilirsiniz yapılandırma parametreleri kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="164d3-235">This object contains the subset of configuration parameters that you can override on a per-controller basis.</span></span> <span data-ttu-id="164d3-236">Değişiklik yapmayın herhangi bir ayarı varsayılan genel **HttpConfiguration** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="164d3-236">Any settings that you don't change default to the global **HttpConfiguration** object.</span></span>