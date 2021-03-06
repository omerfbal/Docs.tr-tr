---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
title: Bir rota kısıtlaması oluşturma (VB) | Microsoft Docs
author: StephenWalther
description: Bu öğreticide, Normal ifadelerle rota kısıtlamalarını oluşturarak tarayıcı eşleşen yolların nasıl istekleri nasıl kontrol edebilir Stephen Walther gösterir.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: b7cce113-c82c-45bf-b97b-357e5d9f7f56
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 0a8e540a00d852d5b710bfdbf63a68f6e6d280ee
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41754677"
---
<a name="creating-a-route-constraint-vb"></a>Bir rota kısıtlaması oluşturma (VB)
====================
tarafından [Stephen Walther](https://github.com/StephenWalther)

> Bu öğreticide, Normal ifadelerle rota kısıtlamalarını oluşturarak tarayıcı eşleşen yolların nasıl istekleri nasıl kontrol edebilir Stephen Walther gösterir.


Rota kısıtlamalarını belirli bir rota ile eşleşmekte tarayıcı istekleri kısıtlamak için kullanın. Rota kısıtlaması belirtmek için normal bir ifade kullanabilirsiniz.

Örneğin, rota, Global.asax dosyasında listeleniyor 1'de tanımladığınız düşünün.

**1 - Global.asax.vb listeleme**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample1.vb)]

Kod 1 ürün adlı bir rota içerir. Tarayıcı istek listeleme 2'de yer alan ProductController eşlemek için ürün yol kullanabilirsiniz.

**2 - Controllers\ProductController.vb listeleme**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample2.vb)]

Ürün denetleyicisi tarafından kullanıma sunulan Details() eylem ProductID adlı tek bir parametre kabul ettiğini dikkat edin. Bu parametre, bir tamsayı parametresidir.

Listeleme 1'de tanımlanan yol, aşağıdaki URL'lerden herhangi birini eşleşmesi:

- / Ürün/23
- Ürün/7

Ne yazık ki, yol aşağıdaki URL'ler eşleşir:

- / Ürün/filan
- / Ürün/apple

Bir tamsayı değeri dışında bir şey içeren bir istekte Details() eylemi bir tam sayı parametresi beklediği hataya neden olur. URL /Product/apple tarayıcınıza yazın örneğin, daha sonra hata sayfası Şekil 1'de alırsınız.


[![Yeni Proje iletişim kutusu](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)

**Şekil 01**: explode bir sayfayı görmeden ([tam boyutlu görüntüyü görmek için tıklatın](creating-a-route-constraint-vb/_static/image2.png))


Ne yapmak istediğinizden, yalnızca uygun tamsayı ProductID içeren URL'ler aynı olur. Rota ile eşleşmekte URL'leri kısıtlamak için bir rota tanımlarken bir kısıtlama kullanabilirsiniz. Yalnızca tamsayılara eşleşen bir normal ifade kısıtlaması listeleme 3'te değiştirilmiş ürün yol içerir.

**3 - Global.asax.vb listeleme**

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample3.vb)]

Normal ifade \d+ tamsayılar bir veya daha fazla eşleşir. Bu sınırlama aşağıdaki URL'ler ile eşleştirilecek ürün yol neden olur:

- / Ürün/3
- / Ürün/8999

Ancak aşağıdaki URL'leri:

- / Ürün/apple
- / Ürün

Bu tarayıcı istekleri başka bir yol tarafından işlenecek veya eşleşen yol yok, ise bir *kaynak bulunamadı* hata döndürülür.

> [!div class="step-by-step"]
> [Önceki](creating-custom-routes-vb.md)
> [İleri](creating-a-custom-route-constraint-vb.md)
