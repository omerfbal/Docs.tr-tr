---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: Bir ASP.NET MVC uygulamasındaki Entity Framework ile ilgili verileri güncelleştirme | Microsoft Docs
author: tdykstra
description: Contoso University örnek web uygulaması Entity Framework 6 Code First ve Visual Studio kullanarak ASP.NET MVC 5 uygulamalarının nasıl oluşturulacağını gösterir...
ms.author: riande
ms.date: 05/01/2015
ms.assetid: 7ba88418-5d0a-437d-b6dc-7c3816d4ec07
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: e7f5fd725a0d151f19f49be9ceaf52b049d459c0
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41754973"
---
<a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application"></a>Bir ASP.NET MVC uygulamasındaki Entity Framework ile ilgili verileri güncelleştirme
====================
tarafından [Tom Dykstra](https://github.com/tdykstra)

[Tamamlanmış projeyi indirmek](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) veya [PDF olarak indirin](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> Contoso University örnek web uygulaması Entity Framework 6 Code First ve Visual Studio 2013 kullanarak ASP.NET MVC 5 uygulamalarının nasıl oluşturulacağını gösterir. Öğretici serisinin hakkında daha fazla bilgi için bkz. [serideki ilk öğreticide](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).


Önceki öğreticide ilgili veriler görüntülenecek; Bu öğreticide ilgili verileri güncelleştirin. Çoğu ilişki için bu yabancı anahtar alanları veya gezinti özelliklerini güncelleştirerek yapılabilir. Varlıklar için ve uygun Gezinti özelliklerinden ekleyip şekilde çoktan çoğa ilişkiler için Entity Framework birleşim tablosundan doğrudan ortaya çıkarmıyor.

Aşağıdaki çizimler ile çalışma sayfaları bazılarını göstermektedir.

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![Kurslarıyla Eğitmen Düzenle](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a>Kursları oluşturma ve düzenleme sayfalarını özelleştirme

Yeni bir kurs varlık oluşturulduğunda, var olan bir bölüm arasında bir ilişki olması gerekir. Bunu kolaylaştırmak için iskele kurulan kodu denetleyici metotları ve departman seçmek için aşağı açılan listede yer oluşturma ve düzenleme görünümleri içerir. Açılır listede kümeleri `Course.DepartmentID` yabancı anahtar özellik ve tüm yük için Entity Framework gereken `Department` uygun sahip gezinme özelliği `Department` varlık. İskele kurulan kodu kullanır ancak biraz hata işleme eklemek ve açılan listeyi sıralamak için değiştirmeniz.

İçinde *CourseController.cs*, dört Sil `Create` ve `Edit` yöntemleri ve bunları aşağıdaki kodla değiştirin:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

Aşağıdaki `using` dosyasının başında deyimi:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`PopulateDepartmentsDropDownList` Yöntemi tüm Departmanlar adına göre sıralanmış bir listesini alır, oluşturur bir `SelectList` koleksiyonu için bir açılan liste ve toplama görünümüne geçirir bir `ViewBag` özelliği. Yöntemi isteğe bağlı olarak kabul `selectedDepartment` açılır listede işlendiğinde seçilir öğeyi belirtmek çağıran kod veren parametresi. Görünüm adı geçer `DepartmentID` için [DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) Yardımcısı ve yardımcı ardından bilir aranacak `ViewBag` nesnesi bir `SelectList` adlı `DepartmentID`.

`HttpGet` `Create` Yöntem çağrılarını `PopulateDepartmentsDropDownList` için yeni bir kurs departman henüz yapılandırılmadı çünkü seçilen öğe ayarlama olmadan yöntemi:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

`HttpGet` `Edit` Yöntemi düzenlenmekte olan kursa zaten atanmış bölüm Kimliğini temel öğeye ayarlar:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

`HttpPost` Hem de yöntemleri `Create` ve `Edit` de bunlar sayfanın bir hatanın ardından yeniden seçili öğe ayarlar kodu içerir:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

Bu kod, her departman seçilen hata mesajını göstermeye sayfası görüntülendiğinde, seçili kalmasını sağlar.

Kurs görünümleri zaten departmanı alanı için aşağı açılır listeler ile iskele kurulmuş, ancak aşağıdaki vurgulanmış yapma değiştirmek için bu alan için DepartmentID açıklamalı alt yazı istemiyorsanız *Views\Course\Create.cshtml* dosya açıklamalı alt yazı değiştirin.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

İçinde aynı değişikliği yapmanız *Views\Course\Edit.cshtml*.

Anahtar değeri veritabanı tarafından oluşturulur ve değiştirilemez ve kullanıcılara gösterilmesi için anlamlı bir değer değildir çünkü iskele kurucu normalde bir birincil anahtar iskelesini değil. Kurs varlıkları için iskele kurucu bir metin kutusu içermez `CourseID` anlar, çünkü alan `DatabaseGeneratedOption.None` özniteliği anlamına gelir kullanıcı mümkün birincil anahtarı değerini girin. Ancak sayı anlamlı olduğundan el ile eklemeniz gerekmez diğer görünümlerde görmek istediğiniz anlamıyor.

İçinde *Views\Course\Edit.cshtml*, önce bir kurs sayı alan eklemek **başlık** alan. Birincil anahtar olduğu için nerde gösterilirse, ancak değiştirilemez.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

Gizli bir alan zaten var. (`Html.HiddenFor` Yardımcısı) düzenleme Görünümü'nde kurs numarası. Ekleme bir *Html.LabelFor* Yardımcısı kullanıcı tıkladığında, deftere nakledilen verileri eklenecek kurs sayısı neden olmayan gizli alan gereksinimini ortadan değil **Kaydet** Düzenle sayfasında.

İçinde *Views\Course\Delete.cshtml* ve *Views\Course\Details.cshtml*önce kursta sayı alanı ekleyin ve "Departman" için "Adından" bölüm adı başlığını değiştirme **başlığı**  alan.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

Çalıştırma **Oluştur** sayfa (kurs dizin sayfasını görüntüleyin ve tıklayın **Yeni Oluştur**) ve yeni bir kurs için veri girin:

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

**Oluştur**'u tıklatın. Listeye eklenen yeni kurs ile kurs dizin sayfası görüntülenir. Bölüm adı dizin sayfası listesinde ilişki doğru şekilde kurulduğundan gösteren navigation özelliğinden gelir.

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

Çalıştırma **Düzenle** sayfa (kurs dizin sayfasını görüntüleyin ve tıklayın **Düzenle** kurs üzerinde).

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Sayfadaki verileri değiştirip'ı **Kaydet**. Güncelleştirilmiş kurs verilerle kurs dizin sayfası görüntülenir.

## <a name="adding-an-edit-page-for-instructors"></a>Eğitmen için bir düzen sayfası ekleme

Bir eğitmen kaydı düzenlediğinizde, eğitmen ofis ataması güncelleştirilecek yönetebilmek istiyorsunuz. `Instructor` Varlığı ile bir sıfır-veya-bir ilişkisi vardır `OfficeAssignment` aşağıdaki durumlarda işlemek gerekir yani varlık:

- Kullanıcı ofis ataması temizler ve ilk olarak bir değer vardı, Sil kaldırın ve gereken `OfficeAssignment` varlık.
- Kullanıcı bir office atama değer girer ve başlangıçta boş ise, yeni bir oluşturmalısınız `OfficeAssignment` varlık.
- Kullanıcı bir ofis ataması değeri değişirse, mevcut değerin değiştirmeli `OfficeAssignment` varlık.

Açık *InstructorController.cs* bakın `HttpGet` `Edit` yöntemi:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

İskele kurulan kodu buraya istediklerinizi değildir. Bu verileri ayarı bir açılan liste, ancak için bir metin kutusu ihtiyacınız olduğu. Bu yöntem, aşağıdaki kodla değiştirin:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

Bu kod bıraktığı `ViewBag` deyimi ve ilişkili istekli yükleme ekler `OfficeAssignment` varlık. İle istekli yükleme gerçekleştiremezsiniz `Find` yöntemi, bu nedenle `Where` ve `Single` yöntemleri yerine Eğitmen seçmek için kullanılır.

Değiştirin `HttpPost` `Edit` yöntemini aşağıdaki kod ile. hangi office atama güncelleştirmelerini işler:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

Başvuru `RetryLimitExceededException` gerektirir bir `using` eklemek için sağ deyimi; `RetryLimitExceededException`ve ardından **çözmek** - **System.Data.Entity.Infrastructurekullanarak**.

![Yeniden deneme özel durumu çözümleyin](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

Kod şunları yapar:

- Yöntem adına değişiklikleri `EditPost` imza artık aynı olduğundan `HttpGet` yöntemi ( `ActionName` özniteliği belirtir /Edit/ URL'si hala kullanılır).
- Geçerli alır `Instructor` istekli yükleme için kullanarak veritabanını bir varlıktan `OfficeAssignment` gezinme özelliği. Bu, yaptığınız aynıdır `HttpGet` `Edit` yöntemi.
- Alınan güncelleştirmeler `Instructor` varlık değerlerle model bağlayıcı. [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) aşırı kullanılan olanak tanır *beyaz liste* dahil etmek istediğiniz özellikler. Bu aşırı posta açıklandığı şekilde engeller [ikinci öğreticide](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- Ofis konumu boş ise, ayarlar `Instructor.OfficeAssignment` özelliği null böylece ilgili satırdaki `OfficeAssignment` tablo silinecek.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- Değişiklikleri veritabanına kaydeder.

İçinde *Views\Instructor\Edit.cshtml*, sonra `div` için öğeleri **işe giriş tarihi** alan, ofis konumu düzenlemek için yeni bir alan ekleyin:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

Sayfayı çalıştırın (seçin **Eğitmenler** sekmesine ve ardından **Düzenle** bir eğitmen üzerinde). Değişiklik **ofis konumu** tıklatıp **Kaydet**.

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a>Eğitmen ekleme kurs atamaları sayfayı Düzenle

Eğitmenler kursları herhangi bir sayıda öğretin. Artık aşağıdaki ekran görüntüsünde gösterildiği gibi bir grup onay kutularını kullanarak kurs atamalarını değiştirme olanağı ekleyerek Eğitmen Düzenle sayfasında geliştirmek:

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

Arasındaki ilişkiyi `Course` ve `Instructor` varlıklar olduğunu çoktan çoğa, birleştirme tabloda yer alan yabancı anahtar özelliklerini doğrudan erişim sahip olmadığınız anlamına gelir. Bunun yerine, ekleyip varlıkları ve ondan `Instructor.Courses` gezinme özelliği.

Hangi kursları değiştirmenize olanak sağlayan bir eğitmen UI'dir atanan onay kutularını grubudur. Her kurs sonunda verilen veritabanında bir onay kutusu görüntülenir ve Eğitmen şu anda atandığı olanları seçilir. Kullanıcı seçin veya kurs atamaları değiştirmek için onay kutularının işaretini kaldırın. Kursları sayısı çok büyük, görünüm verileri sunmak için farklı bir yöntem kullanmak istiyorsunuz, ancak oluşturmak veya ilişkileri silmek için Gezinti özelliklerini düzenleme aynı yöntemini kullanmanız gerekir.

Verileri görüntülemek için onay kutusu listesi sağlamak için bir görünüm modeli sınıfı kullanacaksınız. Oluşturma *AssignedCourseData.cs* içinde *Viewmodel'lar* klasörü ve varolan kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

İçinde *InstructorController.cs*, değiştirin `HttpGet` `Edit` yöntemini aşağıdaki kod ile. Değişiklikler vurgulanır.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

İstekli yükleme için kod ekler `Courses` gezinme özelliğini ve yeni çağırır `PopulateAssignedCourseData` dizi onay kutusunu kullanma hakkında bilgi sağlamak için yöntemi `AssignedCourseData` model sınıfı görüntüleyin.

Kodda `PopulateAssignedCourseData` yöntemi okur ile tüm `Course` varlıklar listesi görünümünü kullanarak kursları yüklemek için model sınıfı. Her kurs için kod kursu Eğitmen içinde mevcut olup olmadığını denetler `Courses` gezinme özelliği. Bir kurs eğitmen için atanmış olup olmadığını denetlerken verimli arama oluşturmak için eğitmen için atanan kursları içine yerleştirilir bir [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) koleksiyonu. `Assigned` Özelliği `true` kursları Eğitmen atanır. Görünüm, bu özellik, hangi onay kutuları olarak görüntülenmelidir seçili belirlemek için kullanır. Son olarak, listenin Görünümü'nde geçirilecek bir `ViewBag` özelliği.

Ardından, kullanıcı tıkladığında yürütülen kod ekleme **Kaydet**. Değiştirin `EditPost` yöntemini aşağıdaki kodla güncelleştirmeleri yeni bir yöntemi çağıran `Courses` gezinti özelliği `Instructor` varlık. Değişiklikler vurgulanır.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

Yöntem imzası farklı `HttpGet` `Edit` yöntemi için yöntem adını değişiklikleri `EditPost` geri `Edit`.

Görünüm koleksiyonunu olmadığı `Course` varlıklar, model bağlayıcı güncelleştiremiyor otomatik olarak `Courses` gezinme özelliği. Güncelleştirilecek model bağlayıcısını kullanmak yerine `Courses` gezinti özelliği, bu yeni gerçekleştirirsiniz `UpdateInstructorCourses` yöntemi. Bu nedenle hariç tutmak ihtiyacınız `Courses` model bağlama özelliği. Bunu çağıran kodu herhangi bir değişiklik gerektirmez [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) kullanmakta olduğunuz çünkü *beyaz listeye ekleme* aşırı yükleme ve `Courses` ekleme listesinde değil.

Onay kutuları seçilmedi, kodda `UpdateInstructorCourses` başlatır `Courses` sahip boş bir koleksiyon gezinme özelliği:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

Kod sonra veritabanındaki tüm kurslara döngü ve her kurs sonunda verilen görünümünde seçilen olanları karşı Eğitmen atanmış olanlar karşı denetler. Verimli aramaları kolaylaştırmak için ikinci iki koleksiyon depolanır `HashSet` nesneleri.

Bir kurs için onay kutusu seçili ancak kursu değil `Instructor.Courses` gezinti özelliği, kurs gezinme özelliğini koleksiyona eklenir.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

Bir kurs için onay kutusu seçili değildi, ancak kursu bulunduğu `Instructor.Courses` Gezinti özelliğine, kurs navigation özelliğinden kaldırılır.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

İçinde *Views\Instructor\Edit.cshtml*, ekleme bir **kursları** aşağıdakileri ekleyerek onay kutularını bir alan hemen sonra kod `div` için öğeleri `OfficeAssignment` alan ve önce `div` öğesi için **Kaydet** düğmesi:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

Yapıştırdıktan sonra burada yaptığınız gibi satır sonlarını, kod ve girinti görünmüyor, burada gördüğünüz gibi görünüyor. böylece her şeyi el ile düzeltin. Girinti mükemmel, olması gerekmez ancak `@</tr><tr>`, `@:<td>`, `@:</td>`, ve `@</tr>` satırları her tek bir satırda gösterilen gibi olmalıdır veya bir çalışma zamanı hatası alırsınız.

Bu kod, üç sütuna sahip bir HTML tablosu oluşturur. Her kurs numarası ve başlığı oluşan bir resim yazısı tarafından izlenen bir onay kutusu sütunundadır. Tüm onay kutularını oldukları bir grup olarak kabul edilmesi için model bağlayıcı bildirir aynı adı ("selectedCourses") sahip. `value` Her onay kutusunun öznitelik değeri olarak ayarlanır `CourseID.` sayfa gönderildiğinde, model bağlayıcı dizisi içeren denetleyicisine geçirir. `CourseID` yalnızca, seçilen onay kutularına için değerler.

Onay kutularını başlangıçta işlendiğinde, eğitmen için atanan kurslara olanlar sahip `checked` öznitelikleri, bunları (bunları kullanıma gösterir) seçer.

Kurs atamaları değiştirdikten sonra site döndüğünde değişiklikleri doğrulamak için isteyebilirsiniz `Index` sayfası. Bu nedenle, bu sayfa tabloda bir sütun eklemeniz gerekir. Bu durumda kullanmanız gerekmez `ViewBag` görüntülemek istediğiniz bilgileri zaten kullanımda olduğundan, nesne `Courses` gezinti özelliği `Instructor` sayfasına model olarak geçirerek varlık.

İçinde *Views\Instructor\Index.cshtml*, ekleme bir **kursları** hemen başlık **Office** aşağıdaki örnekte gösterildiği gibi başlığı:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

Ardından office konumu ayrıntı hücre hemen ardından, yeni bir ayrıntı hücresi ekleyin:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

Çalıştırma **Eğitmen dizin** her eğitmen için atanan kursları görmek için sayfayı:

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

Tıklayın **Düzenle** üzerinde bir eğitmen Düzen sayfasına bakın.

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

Bazı kurs atamalarını değiştirip'ı **Kaydet**. Dizin sayfasında, yaptığınız değişiklikler yansıtılır.

 Not: Burada Eğitmen kurs verileri düzenlemek için uygulanan yaklaşıma de sınırlı sayıda kursları olduğunda çalışır. Farklı bir kullanıcı Arabirimi ve farklı bir güncelleştirme yöntemi, daha büyük olan koleksiyonları için gerekli olacaktır.  
 

## <a name="update-the-deleteconfirmed-method"></a>Güncelleştirme DeleteConfirmed yöntemi

İçinde *InstructorController.cs*, silme `DeleteConfirmed` aşağıdaki kodu yerine yöntemi ve ekleme.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

Bu kod, aşağıdaki değişiklik yapar:

- Eğitmen departmanı Yöneticisi olarak atanmış ise, departmanından Eğitmen atama kaldırır. Bu kod olmadan, bir departman için yönetici olarak atanan bir eğitmen silmeye çalıştığınız bir başvuru bütünlüğü hatası elde edersiniz.

Bu kod, birden çok Departmanlar için yönetici olarak atanan bir eğitmen senaryo işlemiyor. Son öğreticisinde, bu senaryonun oluşmasını engeller kod ekleyeceksiniz.

## <a name="add-office-location-and-courses-to-the-create-page"></a>Ofis konumu ve kurslar oluşturma sayfasına ekleme

İçinde *InstructorController.cs*, silme `HttpGet` ve `HttpPost` `Create` yöntemleri ve bunun yerine aşağıdaki kodu ekleyin:


[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

Bu kod, hiçbir kursları seçilmemesini dışında hangi düzenleme yöntemlerini gördüğünüz için benzer. `HttpGet` `Create` Yöntem çağrılarını `PopulateAssignedCourseData` değil olabileceğinden ancak seçilmiş yöntemi sipariş sağlamak için boş bir koleksiyon için `foreach` (Aksi halde kodu görüntüle throw bir null başvurusu özel durumu görünümünde döngü ).

HttpPost oluşturma yöntemi seçilen her kurs sonunda verilen önce doğrulama hatalarını denetler ve yeni Eğitmen veritabanına ekler şablon kodunu kursları gezinme özelliği ekler. Model hataları olsa bile kursları eklenir böylece model hatalar (için örnek, geçersiz tarih Anahtarlanan kullanıcı) yapılan herhangi bir kurs Seçimi sayfasında bir hata iletisi ile ne zaman yeniden böylece otomatik olarak geri yüklenir.

Kursa eklemeniz mümkün olması için dikkat `Courses` Gezinti özelliğine sahip olarak boş bir koleksiyon özelliğini başlatmak için:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

Denetleyici kodda bunu alternatif olarak, eğitmen modelde mevcut değilse otomatik olarak koleksiyonu aşağıdaki örnekte gösterildiği gibi oluşturmak için özellik Get yordamı değiştirerek bunu:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

Değiştirirseniz `Courses` özelliği bu şekilde, denetleyicinin açık özellik başlatma kodu kaldırabilirsiniz.

İçinde *Views\Instructor\Create.cshtml*, bir office konumu metin kutusu ekleyin ve işe alım alan tarihten ve önce onay kutularını kurs **Gönder** düğmesi.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

Kod yapıştırıldıktan sonra daha önce düzenleme sayfası için yaptığınız gibi satır sonu ve girinti düzeltin.

Oluştur sayfasında çalıştırın ve bir eğitmen ekleyin.

![Eğitmen kurslarıyla oluşturma](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

<a id="transactions"></a>
## <a name="handling-transactions"></a>İşlem işleme

İçinde anlatıldığı gibi [temel CRUD işlevselliği öğretici](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md), varsayılan olarak Entity Framework örtük olarak işlemler uygular. Daha denetlediğiniz--Örneğin, bir işlemde--Entity Framework dışında yapılan işlemler dahil etmek istiyorsanız senaryolar görmek için [işlemleri çalışma](https://msdn.microsoft.com/data/dn456843) MSDN'de.

## <a name="summary"></a>Özet

Bu giriş, ilgili verilerle çalışmaya tamamladınız. Şu ana kadar bu öğreticileri, zaman uyumlu g/ç gerçekleştiren kod ile çalıştım. Zaman uyumsuz kod uygulama tarafından web sunucu kaynaklarını daha verimli bir şekilde kullanma uygulama yapabilir ve sonraki öğreticide yaparsınız.

Lütfen bu öğreticide sevmediğinizi nasıl ve ne geliştirebileceğimiz hakkında geri bildirim bırakın. Yeni konuları da isteyebilirsiniz [Show Me nasıl ile kod](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).

Entity Framework diğer kaynakların bağlantılarını bulunabilir [ASP.NET veri erişimi - önerilen kaynaklar](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Önceki](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [İleri](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
