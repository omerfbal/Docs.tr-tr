---
title: "Anahtar depolama biçimi"
author: tdykstra
description: "Bu belgede ASP.NET Core veri koruma anahtarı depolama alanı biçimi, uygulama ayrıntıları açıklanmaktadır."
keywords: ASP.NET Core, veri koruma, anahtar depolama
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: e8996478-f7bf-4b58-bab4-7fdb5d8556c5
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/implementation/key-storage-format
ms.openlocfilehash: 4ebad05f7d55e954463ce5e277b419a7d6f773c0
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/10/2017
---
# <a name="key-storage-format"></a><span data-ttu-id="8666b-104">Anahtar depolama biçimi</span><span class="sxs-lookup"><span data-stu-id="8666b-104">Key Storage Format</span></span>

<a name="data-protection-implementation-key-storage-format"></a>

<span data-ttu-id="8666b-105">Nesneleri XML gösterimi bekleyen depolanır.</span><span class="sxs-lookup"><span data-stu-id="8666b-105">Objects are stored at rest in XML representation.</span></span> <span data-ttu-id="8666b-106">Anahtar depolama alanı için varsayılan % LOCALAPPDATA%\ASP.NET\DataProtection-Keys\ dizinidir.</span><span class="sxs-lookup"><span data-stu-id="8666b-106">The default directory for key storage is %LOCALAPPDATA%\ASP.NET\DataProtection-Keys\.</span></span>

## <a name="the-key-element"></a><span data-ttu-id="8666b-107">\<Anahtar > öğesi</span><span class="sxs-lookup"><span data-stu-id="8666b-107">The \<key> element</span></span>

<span data-ttu-id="8666b-108">Üst düzey nesnelerindeki anahtar deposu olarak anahtarları mevcut.</span><span class="sxs-lookup"><span data-stu-id="8666b-108">Keys exist as top-level objects in the key repository.</span></span> <span data-ttu-id="8666b-109">Kurala göre filename anahtarlara sahip **anahtarı-{GUID} .xml**, {GUID} anahtarının kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="8666b-109">By convention keys have the filename **key-{guid}.xml**, where {guid} is the id of the key.</span></span> <span data-ttu-id="8666b-110">Her bir dosya tek bir anahtar içerir.</span><span class="sxs-lookup"><span data-stu-id="8666b-110">Each such file contains a single key.</span></span> <span data-ttu-id="8666b-111">Dosya biçimi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="8666b-111">The format of the file is as follows.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<key id="80732141-ec8f-4b80-af9c-c4d2d1ff8901" version="1">
  <creationDate>2015-03-19T23:32:02.3949887Z</creationDate>
  <activationDate>2015-03-19T23:32:02.3839429Z</activationDate>
  <expirationDate>2015-06-17T23:32:02.3839429Z</expirationDate>
  <descriptor deserializerType="{deserializerType}">
    <descriptor>
      <encryption algorithm="AES_256_CBC" />
      <validation algorithm="HMACSHA256" />
      <enc:encryptedSecret decryptorType="{decryptorType}" xmlns:enc="...">
        <encryptedKey>
          <!-- This key is encrypted with Windows DPAPI. -->
          <value>AQAAANCM...8/zeP8lcwAg==</value>
        </encryptedKey>
      </enc:encryptedSecret>
    </descriptor>
  </descriptor>
</key>
```

<span data-ttu-id="8666b-112">\<Anahtar > öğesi aşağıdaki öznitelikler ve alt öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="8666b-112">The \<key> element contains the following attributes and child elements:</span></span>

* <span data-ttu-id="8666b-113">Anahtar kimliği. Bu değer yetkili olarak kabul edilir; yalnızca bir nicety İnsan okunabilirlik için dosya adıdır.</span><span class="sxs-lookup"><span data-stu-id="8666b-113">The key id. This value is treated as authoritative; the filename is simply a nicety for human readability.</span></span>

* <span data-ttu-id="8666b-114">Sürümü \<anahtar > öğesi, şu anda 1'den sabit.</span><span class="sxs-lookup"><span data-stu-id="8666b-114">The version of the \<key> element, currently fixed at 1.</span></span>

* <span data-ttu-id="8666b-115">Anahtarın oluşturma, etkinleştirme ve sona erme tarihleri.</span><span class="sxs-lookup"><span data-stu-id="8666b-115">The key's creation, activation, and expiration dates.</span></span>

* <span data-ttu-id="8666b-116">A \<tanımlayıcısı > Bu anahtarı içinde yer alan kimliği doğrulanmış şifreleme uygulaması hakkında bilgi içeren öğe.</span><span class="sxs-lookup"><span data-stu-id="8666b-116">A \<descriptor> element, which contains information on the authenticated encryption implementation contained within this key.</span></span>

<span data-ttu-id="8666b-117">Yukarıdaki örnekte anahtarın kimliği {80732141-ec8f-4b80-af9c-c4d2d1ff8901} olduğunda, onu oluşturuldu ve 19 Mart 2015 tarihinde etkinleştirildi ve 90 gün ömrü.</span><span class="sxs-lookup"><span data-stu-id="8666b-117">In the above example, the key's id is {80732141-ec8f-4b80-af9c-c4d2d1ff8901}, it was created and activated on March 19, 2015, and it has a lifetime of 90 days.</span></span> <span data-ttu-id="8666b-118">(Bazen etkinleştirme tarihi biraz önce bu örnekte olduğu gibi oluşturma tarihi olabilir.</span><span class="sxs-lookup"><span data-stu-id="8666b-118">(Occasionally the activation date might be slightly before the creation date as in this example.</span></span> <span data-ttu-id="8666b-119">API'ler nasıl çalışır ve uygulamada zararsız nEtki nedeni budur.)</span><span class="sxs-lookup"><span data-stu-id="8666b-119">This is due to a nit in how the APIs work and is harmless in practice.)</span></span>

## <a name="the-descriptor-element"></a><span data-ttu-id="8666b-120">\<Tanımlayıcısı > öğesi</span><span class="sxs-lookup"><span data-stu-id="8666b-120">The \<descriptor> element</span></span>

<span data-ttu-id="8666b-121">Dış \<tanımlayıcısı > öğesi IAuthenticatedEncryptorDescriptorDeserializer uygulayan bir tür bütünleştirilmiş kod tam adı bir öznitelik deserializerType içerir.</span><span class="sxs-lookup"><span data-stu-id="8666b-121">The outer \<descriptor> element contains an attribute deserializerType, which is the assembly-qualified name of a type which implements IAuthenticatedEncryptorDescriptorDeserializer.</span></span> <span data-ttu-id="8666b-122">Bu tür iç okumak için sorumlu olduğu \<tanımlayıcısı > öğesi ve içinde yer alan bilgileri ayrıştırma.</span><span class="sxs-lookup"><span data-stu-id="8666b-122">This type is responsible for reading the inner \<descriptor> element and for parsing the information contained within.</span></span>

<span data-ttu-id="8666b-123">Belirli biçimi \<tanımlayıcısı > öğesi anahtarının kapsüllenmiş kimliği doğrulanmış Şifreleyici uygulama bağlıdır ve her seri durumdan çıkarıcının türü biraz farklı bir biçim bu için bekliyor.</span><span class="sxs-lookup"><span data-stu-id="8666b-123">The particular format of the \<descriptor> element depends on the authenticated encryptor implementation encapsulated by the key, and each deserializer type expects a slightly different format for this.</span></span> <span data-ttu-id="8666b-124">Genel olarak, bu öğe algoritmik bilgilerini yine de içerecektir (adları olan OID, türleri veya benzer) ve gizli anahtar malzemesi.</span><span class="sxs-lookup"><span data-stu-id="8666b-124">In general, though, this element will contain algorithmic information (names, types, OIDs, or similar) and secret key material.</span></span> <span data-ttu-id="8666b-125">Yukarıdaki örnekte, bu anahtarı AES 256 CBC şifreleme + HMACSHA256 doğrulama kaydırılacağını tanımlayıcısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="8666b-125">In the above example, the descriptor specifies that this key wraps AES-256-CBC encryption + HMACSHA256 validation.</span></span>

## <a name="the-encryptedsecret-element"></a><span data-ttu-id="8666b-126">\<EncryptedSecret > öğesi</span><span class="sxs-lookup"><span data-stu-id="8666b-126">The \<encryptedSecret> element</span></span>

<span data-ttu-id="8666b-127">Bir <encryptedSecret> şifrelenmiş gizli anahtar malzemesi içeren öğesi mevcut olması durumunda [REST gizli şifreleme etkinleştirilmiştir](key-encryption-at-rest.md#data-protection-implementation-key-encryption-at-rest).</span><span class="sxs-lookup"><span data-stu-id="8666b-127">An <encryptedSecret> element which contains the encrypted form of the secret key material may be present if [encryption of secrets at rest is enabled](key-encryption-at-rest.md#data-protection-implementation-key-encryption-at-rest).</span></span> <span data-ttu-id="8666b-128">Öznitelik decryptorType IXmlDecryptor uygulayan bir tür bütünleştirilmiş kod tam adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8666b-128">The attribute decryptorType will be the assembly-qualified name of a type which implements IXmlDecryptor.</span></span> <span data-ttu-id="8666b-129">Bu tür iç okumak için sorumlu olduğu <encryptedKey> öğesi ve özgün düz metin kurtarmak için şifre çözme.</span><span class="sxs-lookup"><span data-stu-id="8666b-129">This type is responsible for reading the inner <encryptedKey> element and decrypting it to recover the original plaintext.</span></span>

<span data-ttu-id="8666b-130">İle \<tanımlayıcısı >, belirli biçimi <encryptedSecret> kullanımda çalışmıyorken şifreleme mekanizması öğesi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8666b-130">As with \<descriptor>, the particular format of the <encryptedSecret> element depends on the at-rest encryption mechanism in use.</span></span> <span data-ttu-id="8666b-131">Yukarıdaki örnekte, ana anahtar yorum Windows DPAPI kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="8666b-131">In the above example, the master key is encrypted using Windows DPAPI per the comment.</span></span>

## <a name="the-revocation-element"></a><span data-ttu-id="8666b-132">\<İptal > öğesi</span><span class="sxs-lookup"><span data-stu-id="8666b-132">The \<revocation> element</span></span>

<span data-ttu-id="8666b-133">Üst düzey nesnelerindeki anahtar deposu olarak iptalleri mevcut.</span><span class="sxs-lookup"><span data-stu-id="8666b-133">Revocations exist as top-level objects in the key repository.</span></span> <span data-ttu-id="8666b-134">Kurala göre iptalleri filename sahip **iptal-{zaman damgası} .xml** (için tüm anahtarları, belirli bir tarihten önce iptal etme) veya **iptal-{GUID} .xml** (için belirli bir anahtarı iptal etme).</span><span class="sxs-lookup"><span data-stu-id="8666b-134">By convention revocations have the filename **revocation-{timestamp}.xml** (for revoking all keys before a specific date) or **revocation-{guid}.xml** (for revoking a specific key).</span></span> <span data-ttu-id="8666b-135">Tek bir her dosyayı içeren \<iptal > öğesi.</span><span class="sxs-lookup"><span data-stu-id="8666b-135">Each file contains a single \<revocation> element.</span></span>

<span data-ttu-id="8666b-136">Dosya içeriği için iptalleri tek tek anahtarların olacaktır olarak aşağıda.</span><span class="sxs-lookup"><span data-stu-id="8666b-136">For revocations of individual keys, the file contents will be as below.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<revocation version="1">
  <revocationDate>2015-03-20T22:45:30.2616742Z</revocationDate>
  <key id="eb4fc299-8808-409d-8a34-23fc83d026c9" />
  <reason>human-readable reason</reason>
</revocation>
```

<span data-ttu-id="8666b-137">Bu durumda, yalnızca belirtilen anahtarı iptal edilir.</span><span class="sxs-lookup"><span data-stu-id="8666b-137">In this case, only the specified key is revoked.</span></span> <span data-ttu-id="8666b-138">Anahtar kimliği ise "*", ancak olarak aşağıdaki örnekte, tüm anahtarları, oluşturulma tarihi olan belirtilen iptal tarihinden önce iptal edilir.</span><span class="sxs-lookup"><span data-stu-id="8666b-138">If the key id is "*", however, as in the below example, all keys whose creation date is prior to the specified revocation date are revoked.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<revocation version="1">
  <revocationDate>2015-03-20T15:45:45.7366491-07:00</revocationDate>
  <!-- All keys created before the revocation date are revoked. -->
  <key id="*" />
  <reason>human-readable reason</reason>
</revocation>
```

<span data-ttu-id="8666b-139">\<Neden > öğesi sistem tarafından hiçbir zaman okuyun.</span><span class="sxs-lookup"><span data-stu-id="8666b-139">The \<reason> element is never read by the system.</span></span> <span data-ttu-id="8666b-140">Bu kullanıcı tarafından okunabilen bir iptal nedeni depolamak için yalnızca uygun bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="8666b-140">It is simply a convenient place to store a human-readable reason for revocation.</span></span>