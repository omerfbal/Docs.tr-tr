---
title: ASP.NET Çekirdeği'nde veri koruma
author: rick-anderson
description: Bu belge, çeşitli ASP.NET Core veri koruma konular için içindekiler tablosu olarak görev yapar.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/index
ms.openlocfilehash: 1c38c587956dd99078fa4386c2f4423d784abc60
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277130"
---
# <a name="data-protection-in-aspnet-core"></a>ASP.NET Çekirdeği'nde veri koruma

* [Veri korumaya giriş](xref:security/data-protection/introduction)

* [Veri Koruma API’lerini kullanmaya başlama](xref:security/data-protection/using-data-protection)

* [Tüketici API'leri](xref:security/data-protection/consumer-apis/index)

  * [Tüketici API’lerine genel bakış](xref:security/data-protection/consumer-apis/overview)

  * [Amaç dizeleri](xref:security/data-protection/consumer-apis/purpose-strings)

  * [Amaç hiyerarşisi ve çok kiracılılık](xref:security/data-protection/consumer-apis/purpose-strings-multitenancy)

  * [Karma parolalar](xref:security/data-protection/consumer-apis/password-hashing)

  * [Korumalı yüklerin ömrünü sınırlama](xref:security/data-protection/consumer-apis/limited-lifetime-payloads)

  * [Anahtarları iptal edilen yüklerin korumasını kaldırma](xref:security/data-protection/consumer-apis/dangerous-unprotect)

* [Yapılandırma](xref:security/data-protection/configuration/index)

  * [ASP.NET Core veri korumasını yapılandırma](xref:security/data-protection/configuration/overview)

  * [Varsayılan ayarlar](xref:security/data-protection/configuration/default-settings)

  * [Makine geneli ilke](xref:security/data-protection/configuration/machine-wide-policy)

  * [DI kullanan olmayan senaryolar](xref:security/data-protection/configuration/non-di-scenarios)

* [Genişletilebilirlik API’leri](xref:security/data-protection/extensibility/index)

  * [Çekirdek şifreleme genişletilebilirliği](xref:security/data-protection/extensibility/core-crypto)

  * [Anahtar yönetimi genişletilebilirliği](xref:security/data-protection/extensibility/key-management)

  * [Çeşitli API'ler](xref:security/data-protection/extensibility/misc-apis)

* [Uygulama](xref:security/data-protection/implementation/index)

  * [Kimliği doğrulanmış şifreleme ayrıntıları](xref:security/data-protection/implementation/authenticated-encryption-details)

  * [Alt anahtar türetme ve kimliği doğrulanmış şifreleme](xref:security/data-protection/implementation/subkeyderivation)

  * [Bağlam üst bilgileri](xref:security/data-protection/implementation/context-headers)

  * [Anahtar yönetimi](xref:security/data-protection/implementation/key-management)

  * [Anahtar depolama sağlayıcıları](xref:security/data-protection/implementation/key-storage-providers)

  * [Bekleme durumunda anahtar şifreleme](xref:security/data-protection/implementation/key-encryption-at-rest)

  * [Anahtar değiştirilemezliği ve ayarlar](xref:security/data-protection/implementation/key-immutability)

  * [Anahtar depolama biçimi](xref:security/data-protection/implementation/key-storage-format)

  * [Kısa ömürlü veri koruma sağlayıcıları](xref:security/data-protection/implementation/key-storage-ephemeral)

* [Uyumluluk](xref:security/data-protection/compatibility/index)

  * [ASP.NET değiştirme <machineKey> ASP.NET Core içinde](xref:security/data-protection/compatibility/replacing-machinekey)
