---
title: SignalR HubContext
author: tdykstra
description: Bir hub dışında istemcilere bildirimleri gönderme için ASP.NET Core SignalR HubContext hizmetini kullanmayı öğrenin.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/13/2018
uid: signalr/hubcontext
ms.openlocfilehash: a02588dc98283a375e9deb7c8561c59f6d886eb0
ms.sourcegitcommit: d53e0cc71542b92de867bcce51575b054886f529
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41755675"
---
# <a name="send-messages-from-outside-a-hub"></a>Bir hub dışında ileti gönderme

Tarafından [Mikael Mengistu](https://twitter.com/MikaelM_12)

SignalR hub'ı, SignalR sunucuya bağlı istemcilere ileti göndermek için çekirdek soyutlamadır. Diğer yerlerden uygulama kullanarak ileti göndermek mümkündür `IHubContext` hizmeti. Bu makalede, bir SignalR erişmeye açıklanmaktadır `IHubContext` hub dışında istemcilere bildirimleri göndermek için.

[Görüntüleme veya indirme örnek kodu](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubcontext/sample/) [(karşıdan yükleme)](xref:tutorials/index#how-to-download-a-sample)

## <a name="get-an-instance-of-ihubcontext"></a>Örneği Al `IHubContext`

ASP.NET Core SignalR öğesinde bir örneğini erişebileceğiniz `IHubContext` aracılığıyla bağımlılık ekleme. Örneği ekleyebilir `IHubContext` bir denetleyici, ara yazılım veya diğer DI hizmeti. İstemcilere göndermek için örneği kullanın.

> [!NOTE]
> Bu, ASP.NET tarafından farklıdır 4.x GlobalHost erişim sağlamak için kullanılan SignalR `IHubContext`. ASP.NET Core, bu genel tekil gereksinimini ortadan kaldırır, bir bağımlılık ekleme çerçeve vardır.

### <a name="inject-an-instance-of-ihubcontext-in-a-controller"></a>Bir örneğini ekleme `IHubContext` bir denetleyicide

Örneği ekleyebilir `IHubContext` , oluşturucuya ekleyerek bir denetleyici içinde:

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=12-19,57)]

Şimdi, örneğine erişimi olan `IHubContext`, hub içinde değilmiş gibi hub yöntemlerini çağırabilirsiniz.

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=21-25)]

### <a name="get-an-instance-of-ihubcontext-in-middleware"></a>Bir kopyasını almak `IHubContext` Ara yazılımında

Erişim `IHubContext` ara yazılım ardışık düzenini içinde şu şekilde:

```csharp
app.Use(next => (context) =>
{
    var hubContext = (IHubContext<MyHub>)context
                        .RequestServices
                        .GetServices<IHubContext<MyHub>>();
    //...
});
```

> [!NOTE]
> Ne zaman hub yöntemleri çağrıldığında gelen dışında `Hub` çağırmayla ilgili hiçbir arayan olduğunda, sınıf. Bu nedenle, erişim yoktur `ConnectionId`, `Caller`, ve `Others` özellikleri.

## <a name="related-resources"></a>İlgili kaynaklar

* [Kullanmaya başlama](xref:tutorials/signalr)
* [Merkezler](xref:signalr/hubs)
* [Azure'a Yayımlama](xref:signalr/publish-to-azure-web-app)
