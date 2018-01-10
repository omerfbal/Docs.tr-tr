---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: "Entity Framework 4.0 veritabanı ile ilk Başlarken ve ASP.NET 4 Web Forms - bölüm 4 | Microsoft Docs"
author: tdykstra
description: "Contoso University örnek web uygulaması Entity Framework kullanarak ASP.NET Web Forms uygulamalarının nasıl oluşturulacağını gösterir. Örnek uygulamasıdır..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: 06d129384fc78db21ad1b9224781deab6a0e91a5
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/10/2017
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a><span data-ttu-id="9e901-104">Entity Framework 4.0 veritabanı ile ilk Başlarken ve ASP.NET 4 Web Forms - bölüm 4</span><span class="sxs-lookup"><span data-stu-id="9e901-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 4</span></span>
====================
<span data-ttu-id="9e901-105">tarafından [zel Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="9e901-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="9e901-106">Contoso University örnek web uygulaması Entity Framework 4.0 ve Visual Studio 2010 kullanarak ASP.NET Web Forms uygulamalarının nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e901-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="9e901-107">Eğitmen serisi hakkında daha fazla bilgi için bkz: [serideki ilk öğreticide](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="9e901-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>


## <a name="working-with-related-data"></a><span data-ttu-id="9e901-108">İlgili verileri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="9e901-108">Working with Related Data</span></span>

<span data-ttu-id="9e901-109">Önceki öğreticide kullandığınız `EntityDataSource` denetim filtresi, sıralama ve Grup verileri.</span><span class="sxs-lookup"><span data-stu-id="9e901-109">In the previous tutorial you used the `EntityDataSource` control to filter, sort, and group data.</span></span> <span data-ttu-id="9e901-110">Bu öğreticide görüntülemek ve ilgili verileri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9e901-110">In this tutorial you'll display and update related data.</span></span>

<span data-ttu-id="9e901-111">Eğitmen listesini gösteren Eğitmen sayfası oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9e901-111">You'll create the Instructors page that shows a list of instructors.</span></span> <span data-ttu-id="9e901-112">Bir eğitmen seçtiğinizde, o Eğitmen tarafından öğrettin kurslar listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9e901-112">When you select an instructor, you see a list of courses taught by that instructor.</span></span> <span data-ttu-id="9e901-113">Bir indirmelere seçtiğinizde, Ayrıntılar indirmelere ve öğrenciler indirmelere kayıtlı bir listesi için bkz.</span><span class="sxs-lookup"><span data-stu-id="9e901-113">When you select a course, you see details for the course and a list of students enrolled in the course.</span></span> <span data-ttu-id="9e901-114">Eğitmen adını, işe alma tarihi ve office atama düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e901-114">You can edit the instructor name, hire date, and office assignment.</span></span> <span data-ttu-id="9e901-115">Office atama bir gezinti özelliği üzerinden erişen ayrı bir varlık kümesidir.</span><span class="sxs-lookup"><span data-stu-id="9e901-115">The office assignment is a separate entity set that you access through a navigation property.</span></span>

<span data-ttu-id="9e901-116">Ana veri ayrıntı verileri işaretleme veya kod bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e901-116">You can link master data to detail data in markup or in code.</span></span> <span data-ttu-id="9e901-117">Öğreticinin bu bölümünde, her iki yöntem kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="9e901-117">In this part of the tutorial, you'll use both methods.</span></span>

<span data-ttu-id="9e901-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9e901-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span></span>

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a><span data-ttu-id="9e901-119">Görüntüleme ve bir GridView denetimindeki ilgili varlıkları güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9e901-119">Displaying and Updating Related Entities in a GridView Control</span></span>

<span data-ttu-id="9e901-120">Adlı yeni bir web sayfası oluşturun *Instructors.aspx* kullanan *Site.Master* ana sayfa ve aşağıdaki biçimlendirmeleri eklemek `Content` adlı Denetim `Content2`:</span><span class="sxs-lookup"><span data-stu-id="9e901-120">Create a new web page named *Instructors.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

<span data-ttu-id="9e901-121">Bu biçimlendirme oluşturur bir `EntityDataSource` Eğitmen seçer ve güncellemelerini denetim.</span><span class="sxs-lookup"><span data-stu-id="9e901-121">This markup creates an `EntityDataSource` control that selects instructors and enables updates.</span></span> <span data-ttu-id="9e901-122">`div` Öğesi sağ tarafta daha sonra bir sütun ekleyeceği sol tarafta işlemek için biçimlendirme yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="9e901-122">The `div` element configures markup to render on the left so that you can add a column on the right later.</span></span>

<span data-ttu-id="9e901-123">Arasında `EntityDataSource` biçimlendirme ve kapanış `</div>` etiketi, oluşturan aşağıdaki biçimlendirmeleri eklemek bir `GridView` denetim ve `Label` hata iletileri için kullanacağınız denetimi:</span><span class="sxs-lookup"><span data-stu-id="9e901-123">Between the `EntityDataSource` markup and the closing `</div>` tag, add the following markup that creates a `GridView` control and a `Label` control that you'll use for error messages:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

<span data-ttu-id="9e901-124">Bu `GridView` denetimi satır seçimi sağlar, seçilen satırın açık gri arka plan rengiyle vurgular ve belirtir (daha sonra oluşturacağınız) işleyicileri için `SelectedIndexChanged` ve `Updating` olaylar.</span><span class="sxs-lookup"><span data-stu-id="9e901-124">This `GridView` control enables row selection, highlights the selected row with a light gray background color, and specifies handlers (which you'll create later) for the `SelectedIndexChanged` and `Updating` events.</span></span> <span data-ttu-id="9e901-125">Ayrıca belirtir `PersonID` için `DataKeyNames` özelliği, böylece daha sonra eklersiniz başka bir denetim için seçilen satırın anahtar değeri geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9e901-125">It also specifies `PersonID` for the `DataKeyNames` property, so that the key value of the selected row can be passed to another control that you'll add later.</span></span>

<span data-ttu-id="9e901-126">Bir gezinti özelliği içinde depolanan Eğitmen office atama son sütun içeriyor `Person` varlık ilişkili bir varlıktan geldiğinden.</span><span class="sxs-lookup"><span data-stu-id="9e901-126">The last column contains the instructor's office assignment, which is stored in a navigation property of the `Person` entity because it comes from an associated entity.</span></span> <span data-ttu-id="9e901-127">Dikkat `EditItemTemplate` öğesi belirttiğinden `Eval` yerine `Bind`, çünkü `GridView` denetim doğrudan bağlanamıyor Gezinti özellikleri için bunları güncelleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9e901-127">Notice that the `EditItemTemplate` element specifies `Eval` instead of `Bind`, because the `GridView` control cannot directly bind to navigation properties in order to update them.</span></span> <span data-ttu-id="9e901-128">Kodda office atama güncelleştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="9e901-128">You'll update the office assignment in code.</span></span> <span data-ttu-id="9e901-129">Bunu yapmak için bir başvuru gerekir `TextBox` denetimi ve almak ve giriş kaydetmek `TextBox` denetimin `Init` olay.</span><span class="sxs-lookup"><span data-stu-id="9e901-129">To do that, you'll need a reference to the `TextBox` control, and you'll get and save that in the `TextBox` control's `Init` event.</span></span>

<span data-ttu-id="9e901-130">Aşağıdaki `GridView` denetimi bir `Label` hata iletileri için kullanılan denetim.</span><span class="sxs-lookup"><span data-stu-id="9e901-130">Following the `GridView` control is a `Label` control that's used for error messages.</span></span> <span data-ttu-id="9e901-131">Denetimin `Visible` özelliği `false`, ve görünüm durumu kapalı, böylece etiketi yalnızca zaman kodu bir hata yanıtı görünür kolaylaştırır görünür.</span><span class="sxs-lookup"><span data-stu-id="9e901-131">The control's `Visible` property is `false`, and view state is turned off, so that the label will appear only when code makes it visible in response to an error.</span></span>

<span data-ttu-id="9e901-132">Açık *Instructors.aspx.cs* dosya ve aşağıdakileri ekleyin `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="9e901-132">Open the *Instructors.aspx.cs* file and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

<span data-ttu-id="9e901-133">Özel sınıfı alanına atama metin kutusu için bir başvuru tutmak için hemen kısmi sınıf adı bildirimi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9e901-133">Add a private class field immediately after the partial-class name declaration to hold a reference to the office assignment text box.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

<span data-ttu-id="9e901-134">İçin bir saplama eklemek `SelectedIndexChanged` olay işleyicisi kod için daha sonra eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="9e901-134">Add a stub for the `SelectedIndexChanged` event handler that you'll add code for later.</span></span> <span data-ttu-id="9e901-135">Ayrıca office atama için bir işleyici ekleyin `TextBox` denetimin `Init` olay başvuru depolayabileceğiniz `TextBox` denetim.</span><span class="sxs-lookup"><span data-stu-id="9e901-135">Also add a handler for the office assignment `TextBox` control's `Init` event so that you can store a reference to the `TextBox` control.</span></span> <span data-ttu-id="9e901-136">Bu başvuru gezinti özelliği ile ilişkili varlık güncelleştirmek için girdiğiniz kullanıcı değeri almak için kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9e901-136">You'll use this reference to get the value the user entered in order to update the entity associated with the navigation property.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

<span data-ttu-id="9e901-137">Kullanacağınız `GridView` denetimin `Updating` güncelleştirmek için olay `Location` ilişkilendirilen özellik `OfficeAssignment` varlık.</span><span class="sxs-lookup"><span data-stu-id="9e901-137">You'll use the `GridView` control's `Updating` event to update the `Location` property of the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="9e901-138">Aşağıdaki işleyicisi ekleme `Updating` olay:</span><span class="sxs-lookup"><span data-stu-id="9e901-138">Add the following handler for the `Updating` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

<span data-ttu-id="9e901-139">Kullanıcı tıkladığında bu kodu çalıştırmak **güncelleştirme** içinde bir `GridView` satır.</span><span class="sxs-lookup"><span data-stu-id="9e901-139">This code is run when the user clicks **Update** in a `GridView` row.</span></span> <span data-ttu-id="9e901-140">Kod LINQ to Entities almak için kullanır. `OfficeAssignment` geçerli ilişkili varlık `Person` varlık kullanarak `PersonID` seçilen satırın gelen olay bağımsız değişken.</span><span class="sxs-lookup"><span data-stu-id="9e901-140">The code uses LINQ to Entities to retrieve the `OfficeAssignment` entity that's associated with the current `Person` entity, using the `PersonID` of the selected row from the event argument.</span></span>

<span data-ttu-id="9e901-141">Kod ardından değeri bağlı olarak aşağıdaki eylemlerden birini alır `InstructorOfficeTextBox` denetimi:</span><span class="sxs-lookup"><span data-stu-id="9e901-141">The code then takes one of the following actions depending on the value in the `InstructorOfficeTextBox` control:</span></span>

- <span data-ttu-id="9e901-142">Metin kutusuna bir değer içeriyor ve var olup olmadığını hiç `OfficeAssignment` güncelleştirmek için varlık tane oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9e901-142">If the text box has a value and there's no `OfficeAssignment` entity to update, it creates one.</span></span>
- <span data-ttu-id="9e901-143">Metin kutusuna bir değer içeriyor ve var olan bir `OfficeAssignment` varlık, güncelleştirdiği `Location` özellik değeri.</span><span class="sxs-lookup"><span data-stu-id="9e901-143">If the text box has a value and there's an `OfficeAssignment` entity, it updates the `Location` property value.</span></span>
- <span data-ttu-id="9e901-144">Metin kutusu boş ise ve bir `OfficeAssignment` varlık var, varlık siler.</span><span class="sxs-lookup"><span data-stu-id="9e901-144">If the text box is empty and an `OfficeAssignment` entity exists, it deletes the entity.</span></span>

<span data-ttu-id="9e901-145">Bundan sonra bu değişiklikleri veritabanına kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9e901-145">After this, it saves the changes to the database.</span></span> <span data-ttu-id="9e901-146">Bir özel durum oluşursa, bir hata iletisi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9e901-146">If an exception occurs, it displays an error message.</span></span>

<span data-ttu-id="9e901-147">Sayfayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9e901-147">Run the page.</span></span>

<span data-ttu-id="9e901-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="9e901-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span></span>

<span data-ttu-id="9e901-149">Tıklatın **Düzenle** ve tüm alanları metin kutularına değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9e901-149">Click **Edit** and all fields change to text boxes.</span></span>

<span data-ttu-id="9e901-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="9e901-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span></span>

<span data-ttu-id="9e901-151">Dahil olmak üzere, bu değerleri değiştirmek **Office atama**.</span><span class="sxs-lookup"><span data-stu-id="9e901-151">Change any of these values, including **Office Assignment**.</span></span> <span data-ttu-id="9e901-152">Tıklatın **güncelleştirme** ve listede yansıtılan değişiklikleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9e901-152">Click **Update** and you'll see the changes reflected in the list.</span></span>

## <a name="displaying-related-entities-in-a-separate-control"></a><span data-ttu-id="9e901-153">İlgili varlıklar ayrı bir denetiminde görüntüleme</span><span class="sxs-lookup"><span data-stu-id="9e901-153">Displaying Related Entities in a Separate Control</span></span>

<span data-ttu-id="9e901-154">Eklediğiniz böylece her Eğitmen bir veya daha fazla kurslar öğretmek bir `EntityDataSource` denetim ve `GridView` hangi Eğitmen Eğitmen seçili ile ilişkili kursları listelemek için Denetim `GridView` denetim.</span><span class="sxs-lookup"><span data-stu-id="9e901-154">Each instructor can teach one or more courses, so you'll add an `EntityDataSource` control and a `GridView` control to list the courses associated with whichever instructor is selected in the instructors `GridView` control.</span></span> <span data-ttu-id="9e901-155">Bir başlığı oluşturmak için ve `EntityDataSource` denetiminde kurslar varlıklar için hata iletisi arasında aşağıdaki biçimlendirmeleri eklemek `Label` denetimi ve kapanış `</div>` etiketi:</span><span class="sxs-lookup"><span data-stu-id="9e901-155">To create a heading and the `EntityDataSource` control for courses entities, add the following markup between the error message `Label` control and the closing `</div>` tag:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

<span data-ttu-id="9e901-156">`Where` Parametre değeri içeriyor `PersonID` olan satır seçildiğinde, eğitmen, `InstructorsGridView` denetim.</span><span class="sxs-lookup"><span data-stu-id="9e901-156">The `Where` parameter contains the value of the `PersonID` of the instructor whose row is selected in the `InstructorsGridView` control.</span></span> <span data-ttu-id="9e901-157">`Where` Özelliği, ilişkili tüm alır yazarak bir komut içerir `Person` varlıklardan bir `Course` varlığın `People` gezinti özelliği ve seçer `Course` varlık eksikse ilişkili birini`Person`varlıklarını içeren seçili `PersonID` değeri.</span><span class="sxs-lookup"><span data-stu-id="9e901-157">The `Where` property contains a subselect command that gets all associated `Person` entities from a `Course` entity's `People` navigation property and selects the `Course` entity only if one of the associated `Person` entities contains the selected `PersonID` value.</span></span>

<span data-ttu-id="9e901-158">Oluşturmak için `GridView` denetimi. hemen ardından aşağıdaki biçimlendirmeleri eklemek `CoursesEntityDataSource` denetimi (kapatmadan önce `</div>` etiketi):</span><span class="sxs-lookup"><span data-stu-id="9e901-158">To create the `GridView` control., add the following markup immediately following the `CoursesEntityDataSource` control (before the closing `</div>` tag):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

<span data-ttu-id="9e901-159">Hiçbir Eğitmen seçilirse, hiçbir kurslar görüntülenen bir `EmptyDataTemplate` öğesi eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="9e901-159">Because no courses will be displayed if no instructor is selected, an `EmptyDataTemplate` element is included.</span></span>

<span data-ttu-id="9e901-160">Sayfayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9e901-160">Run the page.</span></span>

<span data-ttu-id="9e901-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="9e901-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span></span>

<span data-ttu-id="9e901-162">Atanan bir veya daha fazla kurslar sahip bir eğitmen seçin ve indirmelere veya kurslar listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9e901-162">Select an instructor who has one or more courses assigned, and the course or courses appear in the list.</span></span> <span data-ttu-id="9e901-163">(Not: birden çok kurslar veritabanı şeması olanak tanısa da veritabanı ile sağlanan test verilerde hiçbir Eğitmen gerçekte birden fazla indirmelere vardır.</span><span class="sxs-lookup"><span data-stu-id="9e901-163">(Note: although the database schema allows multiple courses, in the test data supplied with the database no instructor actually has more than one course.</span></span> <span data-ttu-id="9e901-164">Kurslar veritabanına kendiniz ekleyebileceğiniz kullanarak **Sunucu Gezgini** penceresi veya *CoursesAdd.aspx* sonraki öğreticide ekleyeceksiniz sayfası.)</span><span class="sxs-lookup"><span data-stu-id="9e901-164">You can add courses to the database yourself using the **Server Explorer** window or the *CoursesAdd.aspx* page, which you'll add in a later tutorial.)</span></span>

<span data-ttu-id="9e901-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="9e901-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span></span>

<span data-ttu-id="9e901-166">`CoursesGridView` Denetimi yalnızca birkaç indirmelere alanları gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e901-166">The `CoursesGridView` control shows only a few course fields.</span></span> <span data-ttu-id="9e901-167">Bir indirmelere tüm ayrıntılarını görüntülemek için kullanacağınız bir `DetailsView` denetimi kullanıcının seçtiği indirmelere için.</span><span class="sxs-lookup"><span data-stu-id="9e901-167">To display all the details for a course, you'll use a `DetailsView` control for the course that the user selects.</span></span> <span data-ttu-id="9e901-168">İçinde *Instructors.aspx*, kapattıktan sonra aşağıdaki biçimlendirme eklemek `</div>` etiketi (Bu biçimlendirme yerleştirdiğiniz emin olun **sonra** kapanış div etiketi, önce onu):</span><span class="sxs-lookup"><span data-stu-id="9e901-168">In *Instructors.aspx*, add the following markup after the closing `</div>` tag (make sure you place this markup **after** the closing div tag, not before it):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

<span data-ttu-id="9e901-169">Bu biçimlendirme oluşturur bir `EntityDataSource` bağlı denetim `Courses` varlık kümesi.</span><span class="sxs-lookup"><span data-stu-id="9e901-169">This markup creates an `EntityDataSource` control that's bound to the `Courses` entity set.</span></span> <span data-ttu-id="9e901-170">`Where` Özelliği seçer kullanarak bir indirmelere `CourseID` kursları seçilen satırın değerini `GridView` denetim.</span><span class="sxs-lookup"><span data-stu-id="9e901-170">The `Where` property selects a course using the `CourseID` value of the selected row in the courses `GridView` control.</span></span> <span data-ttu-id="9e901-171">İşaretleme için bir işleyici belirtir `Selected` başka bir düzeyi hiyerarşisinde daha düşük olan, daha sonra Öğrenci dereceleri görüntülemek için kullanacağınız, olayı.</span><span class="sxs-lookup"><span data-stu-id="9e901-171">The markup specifies a handler for the `Selected` event, which you'll use later for displaying student grades, which is another level lower in the hierarchy.</span></span>

<span data-ttu-id="9e901-172">İçinde *Instructors.aspx.cs*, oluşturmak için aşağıdaki saplama `CourseDetailsEntityDataSource_Selected` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9e901-172">In *Instructors.aspx.cs*, create the following stub for the `CourseDetailsEntityDataSource_Selected` method.</span></span> <span data-ttu-id="9e901-173">(Bu saplama daha sonra öğreticide doldurduğunuz; sayfa derlemek ve çalıştırmak için şu an için ihtiyacınız.)</span><span class="sxs-lookup"><span data-stu-id="9e901-173">(You'll fill this stub out later in the tutorial; for now, you need it so that the page will compile and run.)</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

<span data-ttu-id="9e901-174">Sayfayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9e901-174">Run the page.</span></span>

<span data-ttu-id="9e901-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="9e901-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span></span>

<span data-ttu-id="9e901-176">Başlangıçta hiçbir indirmelere seçilmediğinden indirmelere ayrıntı yok vardır.</span><span class="sxs-lookup"><span data-stu-id="9e901-176">Initially there are no course details because no course is selected.</span></span> <span data-ttu-id="9e901-177">Atanmış bir indirmelere sahip bir eğitmen seçin ve ardından bir indirmelere ayrıntıları görmek için seçin.</span><span class="sxs-lookup"><span data-stu-id="9e901-177">Select an instructor who has a course assigned, and then select a course to see the details.</span></span>

<span data-ttu-id="9e901-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="9e901-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span></span>

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a><span data-ttu-id="9e901-179">EntityDataSource kullanılarak "olay ilgili verileri görüntülemek için seçilen"</span><span class="sxs-lookup"><span data-stu-id="9e901-179">Using the EntityDataSource "Selected" Event to Display Related Data</span></span>

<span data-ttu-id="9e901-180">Son olarak, tüm kayıtlı Öğrenciler ve seçili indirmelere için kendi dereceleri göstermek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="9e901-180">Finally, you want to show all of the enrolled students and their grades for the selected course.</span></span> <span data-ttu-id="9e901-181">Bunu yapmak için kullanacağınız `Selected` olayı `EntityDataSource` denetim bağlı indirmelere `DetailsView`.</span><span class="sxs-lookup"><span data-stu-id="9e901-181">To do this, you'll use the `Selected` event of the `EntityDataSource` control bound to the course `DetailsView`.</span></span>

<span data-ttu-id="9e901-182">İçinde *Instructors.aspx*, sonra aşağıdaki biçimlendirmeleri eklemek `DetailsView` denetimi:</span><span class="sxs-lookup"><span data-stu-id="9e901-182">In *Instructors.aspx*, add the following markup after the `DetailsView` control:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

<span data-ttu-id="9e901-183">Bu biçimlendirme oluşturur bir `ListView` Öğrenciler ve seçili indirmelere için kendi dereceleri listesini görüntüleyen denetim.</span><span class="sxs-lookup"><span data-stu-id="9e901-183">This markup creates a `ListView` control that displays a list of students and their grades for the selected course.</span></span> <span data-ttu-id="9e901-184">Databind kodu denetiminde gerekir çünkü hiçbir veri kaynağı belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="9e901-184">No data source is specified because you'll databind the control in code.</span></span> <span data-ttu-id="9e901-185">`EmptyDataTemplate` Öğesi hiçbir indirmelere seçildiğinde görüntülenecek bir ileti sağlar; bu durumda, görüntülemek için hiçbir Öğrenciler vardır.</span><span class="sxs-lookup"><span data-stu-id="9e901-185">The `EmptyDataTemplate` element provides a message to display when no course is selected—in that case, there are no students to display.</span></span> <span data-ttu-id="9e901-186">`LayoutTemplate` Öğesi listesini görüntülemek için bir HTML tablosu oluşturur ve `ItemTemplate` görüntülenecek sütunları belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e901-186">The `LayoutTemplate` element creates an HTML table to display the list, and the `ItemTemplate` specifies the columns to display.</span></span> <span data-ttu-id="9e901-187">Öğrenci Kimliğini ve Öğrenci düzeyde arasındadır `StudentGrade` varlık ve Öğrenci adı olan `Person` Entity Framework kullanılabilmesini varlık `Person` Gezinti özelliğinin `StudentGrade` varlık.</span><span class="sxs-lookup"><span data-stu-id="9e901-187">The student ID and the student grade are from the `StudentGrade` entity, and the student name is from the `Person` entity that the Entity Framework makes available in the `Person` navigation property of the `StudentGrade` entity.</span></span>

<span data-ttu-id="9e901-188">İçinde *Instructors.aspx.cs*, tamamlanmamış çıkış Değiştir `CourseDetailsEntityDataSource_Selected` aşağıdaki kod ile yöntemi:</span><span class="sxs-lookup"><span data-stu-id="9e901-188">In *Instructors.aspx.cs*, replace the stubbed-out `CourseDetailsEntityDataSource_Selected` method with the following code:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

<span data-ttu-id="9e901-189">Bu olay için olay bağımsız değişken bir öğe veya hiçbir şey seçtiyseniz sıfır öğe olan koleksiyon, formdaki seçili verileri sağlar, bir `Course` varlık seçilidir.</span><span class="sxs-lookup"><span data-stu-id="9e901-189">The event argument for this event provides the selected data in the form of a collection, which will have zero items if nothing is selected or one item if a `Course` entity is selected.</span></span> <span data-ttu-id="9e901-190">Varsa bir `Course` varlık seçildiğinde, kodu kullanan `First` koleksiyonu tek bir nesne olarak dönüştürmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="9e901-190">If a `Course` entity is selected, the code uses the `First` method to convert the collection to a single object.</span></span> <span data-ttu-id="9e901-191">Ardından alır `StudentGrade` gezinti özelliği varlıklardan bunları bir koleksiyona dönüştürür ve bağlar `GradesListView` koleksiyonuna denetim.</span><span class="sxs-lookup"><span data-stu-id="9e901-191">It then gets `StudentGrade` entities from the navigation property, converts them to a collection, and binds the `GradesListView` control to the collection.</span></span>

<span data-ttu-id="9e901-192">Bu görüntülenecek dereceleri ancak boş veri şablonu iletisinde sayfasına ilk kez görüntülendiğinden emin olmak istiyoruz yeterlidir ve her bir indirmelere seçilmedi.</span><span class="sxs-lookup"><span data-stu-id="9e901-192">This is sufficient to display grades, but you want to make sure that the message in the empty data template is displayed the first time the page is displayed and whenever a course is not selected.</span></span> <span data-ttu-id="9e901-193">Bunu yapmak için iki yerde çağırmanız aşağıdaki yöntemi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="9e901-193">To do that, create the following method, which you'll call from two places:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

<span data-ttu-id="9e901-194">Bu yeni yöntemi çağırın `Page_Load` sayfası görüntülenirse boş veri şablonu ilk zaman görüntülemek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="9e901-194">Call this new method from the `Page_Load` method to display the empty data template the first time the page is displayed.</span></span> <span data-ttu-id="9e901-195">Ve ondan çağrısı `InstructorsGridView_SelectedIndexChanged` yöntemi bir eğitmen seçildiğinde bu olay tetiklenir olduğundan, yeni kurslar yani yüklenir kurslara `GridView` denetim ve hiçbiri seçili henüz.</span><span class="sxs-lookup"><span data-stu-id="9e901-195">And call it from the `InstructorsGridView_SelectedIndexChanged` method because that event is raised when an instructor is selected, which means new courses are loaded into the courses `GridView` control and none is selected yet.</span></span> <span data-ttu-id="9e901-196">İki çağrıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9e901-196">Here are the two calls:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

<span data-ttu-id="9e901-197">Sayfayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9e901-197">Run the page.</span></span>

<span data-ttu-id="9e901-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="9e901-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span></span>

<span data-ttu-id="9e901-199">Atanmış bir indirmelere sahip bir eğitmen seçin ve ardından indirmelere seçin.</span><span class="sxs-lookup"><span data-stu-id="9e901-199">Select an instructor that has a course assigned, and then select the course.</span></span>

<span data-ttu-id="9e901-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="9e901-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span></span>

<span data-ttu-id="9e901-201">Şimdi ilgili verilerle çalışmak için birkaç şekilde gördünüz.</span><span class="sxs-lookup"><span data-stu-id="9e901-201">You have now seen a few ways to work with related data.</span></span> <span data-ttu-id="9e901-202">Aşağıdaki öğreticide, var olan varlıkları arasındaki ilişkileri ekleme konusunda bilgi edineceksiniz ilişkileri kaldırma ve var olan bir varlığa bir ilişkisi olan yeni bir varlık ekleme.</span><span class="sxs-lookup"><span data-stu-id="9e901-202">In the following tutorial, you'll learn how to add relationships between existing entities, how to remove relationships, and how to add a new entity that has a relationship to an existing entity.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="9e901-203">[Önceki](the-entity-framework-and-aspnet-getting-started-part-3.md)
[sonraki](the-entity-framework-and-aspnet-getting-started-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="9e901-203">[Previous](the-entity-framework-and-aspnet-getting-started-part-3.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-5.md)</span></span>