---
title: "使用 EF Core-資料模型-5 8 的 razor 頁面"
author: rick-anderson
description: "本教學課程中您要新增更多的實體和關聯性，並指定格式、 驗證和資料庫對應規則，以自訂資料模型。"
keywords: "ASP.NET Core，Entity Framework Core，資料註解"
ms.author: riande
manager: wpickett
ms.date: 10/25/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/complex-data-model
ms.openlocfilehash: c2761f79fa4836d29541526782969bb0fd47778b
ms.sourcegitcommit: 6e46abd65973dea796d364a514de9ec2e3e1c1ed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2017
---
# <a name="creating-a-complex-data-model---ef-core-with-razor-pages-tutorial-5-of-8"></a><span data-ttu-id="af694-104">建立複雜的資料模型的 EF 核心 Razor 頁面教學課程 (5 8 個)</span><span class="sxs-lookup"><span data-stu-id="af694-104">Creating a complex data model - EF Core with Razor Pages tutorial (5 of 8)</span></span>

<span data-ttu-id="af694-105">由[Tom Dykstra](https://github.com/tdykstra)和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="af694-105">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="af694-106">先前的教學課程使用過的基本資料模型的三個實體所組成。</span><span class="sxs-lookup"><span data-stu-id="af694-106">The previous tutorials worked with a basic data model that was composed of three entities.</span></span> <span data-ttu-id="af694-107">在本教學課程：</span><span class="sxs-lookup"><span data-stu-id="af694-107">In this tutorial:</span></span>

* <span data-ttu-id="af694-108">會加入更多的實體和關聯性。</span><span class="sxs-lookup"><span data-stu-id="af694-108">More entities and relationships are added.</span></span>
* <span data-ttu-id="af694-109">以指定格式、 驗證和資料庫對應規則自訂資料模型。</span><span class="sxs-lookup"><span data-stu-id="af694-109">The data model is customized by specifying formatting, validation, and database mapping rules.</span></span>

<span data-ttu-id="af694-110">在下圖顯示完成的資料模型的實體類別：</span><span class="sxs-lookup"><span data-stu-id="af694-110">The entity classes for the completed data model is shown in the following illustration:</span></span>

![實體圖表](complex-data-model/_static/diagram.png)

<span data-ttu-id="af694-112">如果您遇到無法解決的問題時，請下載[已完成的應用程式，為此階段](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part5-complex)。</span><span class="sxs-lookup"><span data-stu-id="af694-112">If you run into problems you can't solve, download the [completed app for this stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part5-complex).</span></span>

## <a name="customize-the-data-model-with-attributes"></a><span data-ttu-id="af694-113">自訂屬性的資料模型</span><span class="sxs-lookup"><span data-stu-id="af694-113">Customize the data model with attributes</span></span>

<span data-ttu-id="af694-114">在本節中的資料模型使用屬性自訂。</span><span class="sxs-lookup"><span data-stu-id="af694-114">In this section, the data model is customized using attributes.</span></span>

### <a name="the-datatype-attribute"></a><span data-ttu-id="af694-115">資料類型屬性</span><span class="sxs-lookup"><span data-stu-id="af694-115">The DataType attribute</span></span>

<span data-ttu-id="af694-116">目前的學生頁面就會顯示註冊日期的時間。</span><span class="sxs-lookup"><span data-stu-id="af694-116">The student pages currently displays the time of the enrollment date.</span></span> <span data-ttu-id="af694-117">一般而言，日期欄位會顯示只以日期而不是時間。</span><span class="sxs-lookup"><span data-stu-id="af694-117">Typically, date fields show only the date and not the time.</span></span>

<span data-ttu-id="af694-118">更新*Models/Student.cs*以下列反白顯示程式碼：</span><span class="sxs-lookup"><span data-stu-id="af694-118">Update *Models/Student.cs* with the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_DataType&highlight=3,12-13)]

<span data-ttu-id="af694-119">[DataType](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatypeattribute?view=netframework-4.7.1)屬性會指定資料庫內建型別比更特定的資料類型。</span><span class="sxs-lookup"><span data-stu-id="af694-119">The [DataType](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatypeattribute?view=netframework-4.7.1) attribute specifies a data type that is more specific than the database intrinsic type.</span></span> <span data-ttu-id="af694-120">在此情況下應該顯示的日期，不的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="af694-120">In this case only the date should be displayed, not the date and time.</span></span> <span data-ttu-id="af694-121">[DataType 列舉](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatype?view=netframework-4.7.1)提供許多的資料類型，例如日期、 時間、 電話號碼、 貨幣、 EmailAddress 等等。`DataType`屬性也可以啟用應用程式會自動提供特定類型的功能。</span><span class="sxs-lookup"><span data-stu-id="af694-121">The [DataType Enumeration](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatype?view=netframework-4.7.1) provides for many data types, such as Date, Time, PhoneNumber, Currency, EmailAddress, etc. The `DataType` attribute can also enable the app to automatically provide type-specific features.</span></span> <span data-ttu-id="af694-122">例如: </span><span class="sxs-lookup"><span data-stu-id="af694-122">For example:</span></span>

* <span data-ttu-id="af694-123">`mailto:`連結會自動建立`DataType.EmailAddress`。</span><span class="sxs-lookup"><span data-stu-id="af694-123">The `mailto:` link is automatically created for `DataType.EmailAddress`.</span></span>
* <span data-ttu-id="af694-124">日期選擇器提供`DataType.Date`大部分的瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="af694-124">The date selector is provided for `DataType.Date` in most browsers.</span></span>

<span data-ttu-id="af694-125">`DataType`屬性發出 HTML 5 `data-` HTML 5 瀏覽器使用的 (唸成的資料 dash) 屬性。</span><span class="sxs-lookup"><span data-stu-id="af694-125">The `DataType` attribute emits HTML 5 `data-` (pronounced data dash) attributes that HTML 5 browsers consume.</span></span> <span data-ttu-id="af694-126">`DataType`屬性是否提供驗證。</span><span class="sxs-lookup"><span data-stu-id="af694-126">The `DataType` attributes do not provide validation.</span></span>

<span data-ttu-id="af694-127">`DataType.Date` 未指定顯示日期的格式。</span><span class="sxs-lookup"><span data-stu-id="af694-127">`DataType.Date` does not specify the format of the date that is displayed.</span></span> <span data-ttu-id="af694-128">根據預設，[日期] 欄位會顯示根據基礎在伺服器上的預設格式[CultureInfo](https://docs.microsoft.com/aspnet/core/fundamentals/localization#provide-localized-resources-for-the-languages-and-cultures-you-support)。</span><span class="sxs-lookup"><span data-stu-id="af694-128">By default, the date field is displayed according to the default formats based on the server's [CultureInfo](https://docs.microsoft.com/aspnet/core/fundamentals/localization#provide-localized-resources-for-the-languages-and-cultures-you-support).</span></span>

<span data-ttu-id="af694-129">`DisplayFormat` 屬性用來明確指定日期格式：</span><span class="sxs-lookup"><span data-stu-id="af694-129">The `DisplayFormat` attribute is used to explicitly specify the date format:</span></span>

```csharp
[DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

<span data-ttu-id="af694-130">`ApplyFormatInEditMode`設定可讓您指定的格式應該也會套用至編輯 UI。</span><span class="sxs-lookup"><span data-stu-id="af694-130">The `ApplyFormatInEditMode` setting specifies that the formatting should also be applied to the edit UI.</span></span> <span data-ttu-id="af694-131">某些欄位不應該使用`ApplyFormatInEditMode`。</span><span class="sxs-lookup"><span data-stu-id="af694-131">Some fields should not use `ApplyFormatInEditMode`.</span></span> <span data-ttu-id="af694-132">例如，貨幣符號應該通常不會顯示在 [編輯] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="af694-132">For example, the currency symbol should generally not be displayed in an edit text box.</span></span>

<span data-ttu-id="af694-133">`DisplayFormat`屬性可由本身。</span><span class="sxs-lookup"><span data-stu-id="af694-133">The `DisplayFormat` attribute can be used by itself.</span></span> <span data-ttu-id="af694-134">它通常是最好使用`DataType`屬性附帶`DisplayFormat`屬性。</span><span class="sxs-lookup"><span data-stu-id="af694-134">It's generally a good idea to use the `DataType` attribute with the `DisplayFormat` attribute.</span></span> <span data-ttu-id="af694-135">`DataType`屬性提供的語意，而不是如何呈現在螢幕上的資料。</span><span class="sxs-lookup"><span data-stu-id="af694-135">The `DataType` attribute conveys the semantics of the data as opposed to how to render it on a screen.</span></span> <span data-ttu-id="af694-136">`DataType`屬性會提供下列優點，不適用於`DisplayFormat`:</span><span class="sxs-lookup"><span data-stu-id="af694-136">The `DataType` attribute provides the following benefits that are not available in `DisplayFormat`:</span></span>

* <span data-ttu-id="af694-137">瀏覽器可以啟用 HTML5 功能。</span><span class="sxs-lookup"><span data-stu-id="af694-137">The browser can enable HTML5 features.</span></span> <span data-ttu-id="af694-138">例如，顯示日曆控制項、 地區設定適當的貨幣符號、 電子郵件連結、 用戶端輸入的驗證等。</span><span class="sxs-lookup"><span data-stu-id="af694-138">For example, show a calendar control, the locale-appropriate currency symbol, email links, client-side input validation, etc.</span></span>
* <span data-ttu-id="af694-139">根據預設，瀏覽器會呈現資料使用正確的格式會根據地區設定。</span><span class="sxs-lookup"><span data-stu-id="af694-139">By default, the browser renders data using the correct format based on the locale.</span></span>

<span data-ttu-id="af694-140">如需詳細資訊，請參閱[\<輸入 > 標記協助程式文件](xref:mvc/views/working-with-forms#the-input-tag-helper)。</span><span class="sxs-lookup"><span data-stu-id="af694-140">For more information, see the [\<input> Tag Helper documentation](xref:mvc/views/working-with-forms#the-input-tag-helper).</span></span>

<span data-ttu-id="af694-141">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="af694-141">Run the app.</span></span> <span data-ttu-id="af694-142">瀏覽至學生索引頁面。</span><span class="sxs-lookup"><span data-stu-id="af694-142">Navigate to the Students Index page.</span></span> <span data-ttu-id="af694-143">不會再顯示的時間。</span><span class="sxs-lookup"><span data-stu-id="af694-143">Times are no longer displayed.</span></span> <span data-ttu-id="af694-144">使用的每個檢視`Student`模型就會顯示不含時間日期。</span><span class="sxs-lookup"><span data-stu-id="af694-144">Every view that uses the `Student` model displays the date without time.</span></span>

![顯示不含時間日期的學生索引頁面](complex-data-model/_static/dates-no-times.png)

### <a name="the-stringlength-attribute"></a><span data-ttu-id="af694-146">StringLength 屬性</span><span class="sxs-lookup"><span data-stu-id="af694-146">The StringLength attribute</span></span>

<span data-ttu-id="af694-147">資料驗證規則和驗證錯誤訊息可以使用屬性來指定。</span><span class="sxs-lookup"><span data-stu-id="af694-147">Data validation rules and validation error messages can be specified with attributes.</span></span> <span data-ttu-id="af694-148">[StringLength](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.stringlengthattribute?view=netframework-4.7.1)屬性會指定字元資料欄位中允許的最小和最大長度。</span><span class="sxs-lookup"><span data-stu-id="af694-148">The [StringLength](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.stringlengthattribute?view=netframework-4.7.1) attribute specifies the minimum and maximum length of characters that are allowed in a data field.</span></span> <span data-ttu-id="af694-149">`StringLength`屬性也會提供用戶端和伺服器端驗證。</span><span class="sxs-lookup"><span data-stu-id="af694-149">The `StringLength` attribute also provides client-side and server-side validation.</span></span> <span data-ttu-id="af694-150">最小值的資料庫結構描述沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="af694-150">The minimum value has no impact on the database schema.</span></span>

<span data-ttu-id="af694-151">更新`Student`包含下列程式碼的模型：</span><span class="sxs-lookup"><span data-stu-id="af694-151">Update the `Student` model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_StringLength&highlight=10,12)]

<span data-ttu-id="af694-152">名稱不能超過 50 個字元限制為上述的程式碼。</span><span class="sxs-lookup"><span data-stu-id="af694-152">The preceding code limits names to no more than 50 characters.</span></span> <span data-ttu-id="af694-153">`StringLength`屬性不會防止使用者輸入名稱的泛空白字元。</span><span class="sxs-lookup"><span data-stu-id="af694-153">The `StringLength` attribute doesn't prevent a user from entering white space for a name.</span></span> <span data-ttu-id="af694-154">[RegularExpression](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.regularexpressionattribute?view=netframework-4.7.1)屬性用來將限制套用至輸入。</span><span class="sxs-lookup"><span data-stu-id="af694-154">The [RegularExpression](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.regularexpressionattribute?view=netframework-4.7.1) attribute is used to apply restrictions to the input.</span></span> <span data-ttu-id="af694-155">例如，下列程式碼需要第一個字元是大寫，而其餘字元是依字母順序排列：</span><span class="sxs-lookup"><span data-stu-id="af694-155">For example, the following code requires the first character to be upper case and the remaining characters to be alphabetical:</span></span>

```csharp
[RegularExpression(@"^[A-Z]+[a-zA-Z''-'\s]*$")]
```

<span data-ttu-id="af694-156">執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="af694-156">Run the app:</span></span>

* <span data-ttu-id="af694-157">瀏覽至學生頁面。</span><span class="sxs-lookup"><span data-stu-id="af694-157">Navigate to the Students page.</span></span>
* <span data-ttu-id="af694-158">選取**新建**，並輸入的名稱長度超過 50 個字元。</span><span class="sxs-lookup"><span data-stu-id="af694-158">Select **Create New**, and enter a name longer than 50 characters.</span></span>
* <span data-ttu-id="af694-159">選取**建立**，用戶端驗證顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="af694-159">Select **Create**, client-side validation shows an error message.</span></span>

![學生索引頁面顯示字串長度錯誤](complex-data-model/_static/string-length-errors.png)

<span data-ttu-id="af694-161">在**SQL Server 物件總管**(SSOX)，按兩下開啟學生資料表設計工具**學生**資料表。</span><span class="sxs-lookup"><span data-stu-id="af694-161">In **SQL Server Object Explorer** (SSOX), open the Student table designer by double-clicking the **Student** table.</span></span>

![移轉之前，在 SSOX students 資料表](complex-data-model/_static/ssox-before-migration.png)

<span data-ttu-id="af694-163">上述影像中顯示的結構描述`Student`資料表。</span><span class="sxs-lookup"><span data-stu-id="af694-163">The preceding image shows the schema for the `Student` table.</span></span> <span data-ttu-id="af694-164">名稱欄位有類型`nvarchar(MAX)`因為尚未在資料庫上執行移轉。</span><span class="sxs-lookup"><span data-stu-id="af694-164">The name fields have type `nvarchar(MAX)` because migrations has not been run on the DB.</span></span> <span data-ttu-id="af694-165">移轉作業執行時稍後在本教學課程中，名稱欄位會成為`nvarchar(50)`。</span><span class="sxs-lookup"><span data-stu-id="af694-165">When migrations are run later in this tutorial, the name fields become `nvarchar(50)`.</span></span>

### <a name="the-column-attribute"></a><span data-ttu-id="af694-166">資料行屬性</span><span class="sxs-lookup"><span data-stu-id="af694-166">The Column attribute</span></span>

<span data-ttu-id="af694-167">屬性可以控制如何對應到資料庫的類別和屬性。</span><span class="sxs-lookup"><span data-stu-id="af694-167">Attributes can control how classes and properties are mapped to the database.</span></span> <span data-ttu-id="af694-168">在本節中，`Column`屬性用來對應名稱`FirstMidName`DB 中的"FirstName"的屬性。</span><span class="sxs-lookup"><span data-stu-id="af694-168">In this section, the `Column` attribute is used to map the name of the `FirstMidName` property to "FirstName" in the DB.</span></span>

<span data-ttu-id="af694-169">建立資料庫時，在模型上的屬性名稱會用於資料行名稱 (除非`Column`屬性使用)。</span><span class="sxs-lookup"><span data-stu-id="af694-169">When the DB is created, property names on the model are used for column names (except when the `Column` attribute is used).</span></span>

<span data-ttu-id="af694-170">`Student`模型使用`FirstMidName`，第一個名稱欄位，因為欄位也可能包含中間名。</span><span class="sxs-lookup"><span data-stu-id="af694-170">The `Student` model uses `FirstMidName` for the first-name field because the field might also contain a middle name.</span></span>

<span data-ttu-id="af694-171">更新*Student.cs*以下列反白顯示的程式碼檔案：</span><span class="sxs-lookup"><span data-stu-id="af694-171">Update the *Student.cs* file with the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Column&highlight=4,14)]

<span data-ttu-id="af694-172">與上述變更，`Student.FirstMidName`應用程式中對應至`FirstName`資料行`Student`資料表。</span><span class="sxs-lookup"><span data-stu-id="af694-172">With the preceding change, `Student.FirstMidName` in the app maps to the `FirstName` column of the `Student` table.</span></span>

<span data-ttu-id="af694-173">新增`Column`屬性變更模型支援`SchoolContext`。</span><span class="sxs-lookup"><span data-stu-id="af694-173">The addition of the `Column` attribute changes the model backing the `SchoolContext`.</span></span> <span data-ttu-id="af694-174">模型支援`SchoolContext`不再符合資料庫。</span><span class="sxs-lookup"><span data-stu-id="af694-174">The model backing the `SchoolContext` no longer matches the database.</span></span> <span data-ttu-id="af694-175">如果套用移轉之前執行的應用程式，則會產生下列例外狀況：</span><span class="sxs-lookup"><span data-stu-id="af694-175">If the app is run before applying migrations, the following exception is generated:</span></span>

```SQL
SqlException: Invalid column name 'FirstName'.
```
<span data-ttu-id="af694-176">若要更新資料庫：</span><span class="sxs-lookup"><span data-stu-id="af694-176">To update the DB:</span></span>

* <span data-ttu-id="af694-177">建置專案。</span><span class="sxs-lookup"><span data-stu-id="af694-177">Build the project.</span></span>
* <span data-ttu-id="af694-178">專案資料夾中，開啟命令視窗。</span><span class="sxs-lookup"><span data-stu-id="af694-178">Open a command window in the project folder.</span></span> <span data-ttu-id="af694-179">輸入下列命令來建立新的移轉，並更新資料庫：</span><span class="sxs-lookup"><span data-stu-id="af694-179">Enter the following commands to create a new migration and update the DB:</span></span>

    ```console
    dotnet ef migrations add ColumnFirstName
    dotnet ef database update
    ```

<span data-ttu-id="af694-180">`dotnet ef migrations add ColumnFirstName`命令會產生下列警告訊息：</span><span class="sxs-lookup"><span data-stu-id="af694-180">The `dotnet ef migrations add ColumnFirstName` command generates the following warning message:</span></span>

```text
An operation was scaffolded that may result in the loss of data.
Please review the migration for accuracy.
```

<span data-ttu-id="af694-181">會產生警告，因為現在的名稱欄位限制為 50 個字元。</span><span class="sxs-lookup"><span data-stu-id="af694-181">The warning is generated because the name fields are now limited to 50 characters.</span></span> <span data-ttu-id="af694-182">如果資料庫中的名稱具有超過 50 個字元，將會遺失最後一個字元 51。</span><span class="sxs-lookup"><span data-stu-id="af694-182">If a name in the DB had more than 50 characters, the 51 to last character would be lost.</span></span>

* <span data-ttu-id="af694-183">測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="af694-183">Test the app.</span></span>

<span data-ttu-id="af694-184">開啟 SSOX 學生資料表：</span><span class="sxs-lookup"><span data-stu-id="af694-184">Open the Student table in SSOX:</span></span>

![在移轉之後，在 SSOX students 資料表](complex-data-model/_static/ssox-after-migration.png)

<span data-ttu-id="af694-186">名稱資料行已套用移轉之前，都型別的[nvarchar （max)](https://docs.microsoft.com/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="af694-186">Before migration was applied, the name columns were of type [nvarchar(MAX)](https://docs.microsoft.com/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql).</span></span> <span data-ttu-id="af694-187">名稱資料行現在會`nvarchar(50)`。</span><span class="sxs-lookup"><span data-stu-id="af694-187">The name columns are now `nvarchar(50)`.</span></span> <span data-ttu-id="af694-188">資料行名稱已經從`FirstMidName`至`FirstName`。</span><span class="sxs-lookup"><span data-stu-id="af694-188">The column name has changed from `FirstMidName` to `FirstName`.</span></span>

> [!Note]
> <span data-ttu-id="af694-189">下一節，在某些階段建置的應用程式會產生編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="af694-189">In the following section, building the app at some stages generates compiler errors.</span></span> <span data-ttu-id="af694-190">指示可指定何時要建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="af694-190">The instructions specify when to build the app.</span></span>

## <a name="student-entity-update"></a><span data-ttu-id="af694-191">學生實體更新</span><span class="sxs-lookup"><span data-stu-id="af694-191">Student entity update</span></span>

![學生實體](complex-data-model/_static/student-entity.png)

<span data-ttu-id="af694-193">更新*Models/Student.cs*為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="af694-193">Update *Models/Student.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_BeforeInheritance&highlight=11,13,15,18,22,24-31)]

### <a name="the-required-attribute"></a><span data-ttu-id="af694-194">必要的屬性</span><span class="sxs-lookup"><span data-stu-id="af694-194">The Required attribute</span></span>

<span data-ttu-id="af694-195">`Required`屬性會讓名稱屬性的必要的欄位。</span><span class="sxs-lookup"><span data-stu-id="af694-195">The `Required` attribute makes the name properties required fields.</span></span> <span data-ttu-id="af694-196">`Required`屬性不需要不可為 null 的類型，例如實值類型 (`DateTime`， `int`，`double`等。)。</span><span class="sxs-lookup"><span data-stu-id="af694-196">The `Required` attribute is not needed for non-nullable types such as value types (`DateTime`, `int`, `double`, etc.).</span></span> <span data-ttu-id="af694-197">不可為 null 的型別會自動視為必要欄位。</span><span class="sxs-lookup"><span data-stu-id="af694-197">Types that can't be null are automatically treated as required fields.</span></span>

<span data-ttu-id="af694-198">`Required`屬性無法取代中的最小長度參數`StringLength`屬性：</span><span class="sxs-lookup"><span data-stu-id="af694-198">The `Required` attribute could be replaced with a minimum length parameter in the `StringLength` attribute:</span></span>

```csharp
[Display(Name = "Last Name")]
[StringLength(50, MinimumLength=1)]
public string LastName { get; set; }
```

### <a name="the-display-attribute"></a><span data-ttu-id="af694-199">顯示屬性</span><span class="sxs-lookup"><span data-stu-id="af694-199">The Display attribute</span></span>

<span data-ttu-id="af694-200">`Display`屬性指定的標題文字方塊中應該是 「 名字 」、 「 姓氏 」、 「 完整名稱 」 和 「 註冊日期 」。</span><span class="sxs-lookup"><span data-stu-id="af694-200">The `Display` attribute specifies that the caption for the text boxes should be "First Name", "Last Name", "Full Name", and "Enrollment Date."</span></span> <span data-ttu-id="af694-201">預設標題已經沒有空間分割單字，例如"Lastname"。</span><span class="sxs-lookup"><span data-stu-id="af694-201">The default captions had no space dividing the words, for example "Lastname."</span></span>

### <a name="the-fullname-calculated-property"></a><span data-ttu-id="af694-202">計算的 FullName 屬性</span><span class="sxs-lookup"><span data-stu-id="af694-202">The FullName calculated property</span></span>

<span data-ttu-id="af694-203">`FullName`是傳回值，由串連兩個其他屬性的導出的屬性。</span><span class="sxs-lookup"><span data-stu-id="af694-203">`FullName` is a calculated property that returns a value that's created by concatenating two other properties.</span></span> <span data-ttu-id="af694-204">`FullName`無法設定，它有只有 get 存取子。</span><span class="sxs-lookup"><span data-stu-id="af694-204">`FullName` cannot be set, it has only a get accessor.</span></span> <span data-ttu-id="af694-205">否`FullName`資料庫中建立資料行。</span><span class="sxs-lookup"><span data-stu-id="af694-205">No `FullName` column is created in the database.</span></span>

## <a name="create-the-instructor-entity"></a><span data-ttu-id="af694-206">建立 [Instructor] 實體</span><span class="sxs-lookup"><span data-stu-id="af694-206">Create the Instructor Entity</span></span>

![Instructor 實體](complex-data-model/_static/instructor-entity.png)

<span data-ttu-id="af694-208">建立*Models/Instructor.cs*為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="af694-208">Create *Models/Instructor.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Instructor.cs?name=snippet_BeforeInheritance)]

<span data-ttu-id="af694-209">請注意一些屬性，在相同`Student`和`Instructor`實體。</span><span class="sxs-lookup"><span data-stu-id="af694-209">Notice that several properties are the same in the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="af694-210">實作繼承教學課程稍後在本系列中，此程式碼已重構消除重複性。</span><span class="sxs-lookup"><span data-stu-id="af694-210">In the Implementing Inheritance tutorial later in this series, this code is refactored to eliminate the redundancy.</span></span>

<span data-ttu-id="af694-211">多個屬性可以在同一行。</span><span class="sxs-lookup"><span data-stu-id="af694-211">Multiple attributes can be on one line.</span></span> <span data-ttu-id="af694-212">`HireDate`可以寫入屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="af694-212">The `HireDate` attributes could be written as follows:</span></span>

```csharp
[DataType(DataType.Date),Display(Name = "Hire Date"),DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

### <a name="the-courseassignments-and-officeassignment-navigation-properties"></a><span data-ttu-id="af694-213">CourseAssignments 和 OfficeAssignment 的導覽屬性</span><span class="sxs-lookup"><span data-stu-id="af694-213">The CourseAssignments and OfficeAssignment navigation properties</span></span>

<span data-ttu-id="af694-214">`CourseAssignments`和`OfficeAssignment`屬性為導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="af694-214">The `CourseAssignments` and `OfficeAssignment` properties are navigation properties.</span></span>

<span data-ttu-id="af694-215">講師可以教導任意數目的課程，因此`CourseAssignments`定義為集合。</span><span class="sxs-lookup"><span data-stu-id="af694-215">An instructor can teach any number of courses, so `CourseAssignments` is defined as a collection.</span></span>

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

<span data-ttu-id="af694-216">如果導覽屬性會保留多個實體：</span><span class="sxs-lookup"><span data-stu-id="af694-216">If a navigation property holds multiple entities:</span></span>

* <span data-ttu-id="af694-217">它必須是清單型別其中項目可以新增、 刪除和更新。</span><span class="sxs-lookup"><span data-stu-id="af694-217">It must be a list type where the entries can be added, deleted, and updated.</span></span>

<span data-ttu-id="af694-218">瀏覽內容類型包括：</span><span class="sxs-lookup"><span data-stu-id="af694-218">Navigation property types include:</span></span>

* `ICollection<T>`
*  `List<T>`
*  `HashSet<T>`

<span data-ttu-id="af694-219">如果`ICollection<T>`指定，則會建立 EF 核心`HashSet<T>`預設集合。</span><span class="sxs-lookup"><span data-stu-id="af694-219">If `ICollection<T>` is specified, EF Core creates a `HashSet<T>` collection by default.</span></span>

<span data-ttu-id="af694-220">`CourseAssignment`實體是一節所述的多對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="af694-220">The `CourseAssignment` entity is explained in the section on many-to-many relationships.</span></span>

<span data-ttu-id="af694-221">Contoso 大學商務規則講師可以有最多一個辦事處的狀態。</span><span class="sxs-lookup"><span data-stu-id="af694-221">Contoso University business rules state that an instructor can have at most one office.</span></span> <span data-ttu-id="af694-222">`OfficeAssignment`屬性會保留單一`OfficeAssignment`實體。</span><span class="sxs-lookup"><span data-stu-id="af694-222">The `OfficeAssignment` property holds a single `OfficeAssignment` entity.</span></span> <span data-ttu-id="af694-223">`OfficeAssignment`如果沒有 office 會指派，為 null。</span><span class="sxs-lookup"><span data-stu-id="af694-223">`OfficeAssignment` is null if no office is assigned.</span></span>

```csharp
public OfficeAssignment OfficeAssignment { get; set; }
```

## <a name="create-the-officeassignment-entity"></a><span data-ttu-id="af694-224">建立 OfficeAssignment 實體</span><span class="sxs-lookup"><span data-stu-id="af694-224">Create the OfficeAssignment entity</span></span>

![OfficeAssignment 實體](complex-data-model/_static/officeassignment-entity.png)

<span data-ttu-id="af694-226">建立*Models/OfficeAssignment.cs*為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="af694-226">Create *Models/OfficeAssignment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/OfficeAssignment.cs)]

### <a name="the-key-attribute"></a><span data-ttu-id="af694-227">索引鍵屬性</span><span class="sxs-lookup"><span data-stu-id="af694-227">The Key attribute</span></span>

<span data-ttu-id="af694-228">`[Key]`屬性用來識別屬性的主索引鍵 (PK) 的屬性名稱任務在身時以外 classnameID 或識別碼。</span><span class="sxs-lookup"><span data-stu-id="af694-228">The `[Key]` attribute is used to identify a property as the primary key (PK) when the property name is something other than classnameID or ID.</span></span>

<span data-ttu-id="af694-229">以 0 或-1 一個之間沒有關聯性`Instructor`和`OfficeAssignment`實體。</span><span class="sxs-lookup"><span data-stu-id="af694-229">There's a one-to-zero-or-one relationship between the `Instructor` and `OfficeAssignment` entities.</span></span> <span data-ttu-id="af694-230">相對於指派給講師只存在 office 指派。</span><span class="sxs-lookup"><span data-stu-id="af694-230">An office assignment only exists in relation to the instructor it's assigned to.</span></span> <span data-ttu-id="af694-231">`OfficeAssignment` PK 也是其外部索引鍵 (FK) 至`Instructor`實體。</span><span class="sxs-lookup"><span data-stu-id="af694-231">The `OfficeAssignment` PK is also its foreign key (FK) to the `Instructor` entity.</span></span> <span data-ttu-id="af694-232">無法自動辨識 EF 核心`InstructorID`為的 PK`OfficeAssignment`因為：</span><span class="sxs-lookup"><span data-stu-id="af694-232">EF Core can't automatically recognize `InstructorID` as the PK of `OfficeAssignment` because:</span></span>

* <span data-ttu-id="af694-233">`InstructorID`未遵循識別碼或 classnameID 命名慣例。</span><span class="sxs-lookup"><span data-stu-id="af694-233">`InstructorID` doesn't follow the ID or classnameID naming convention.</span></span>

<span data-ttu-id="af694-234">因此，`Key`屬性用來識別`InstructorID`PK 為：</span><span class="sxs-lookup"><span data-stu-id="af694-234">Therefore, the `Key` attribute is used to identify `InstructorID` as the PK:</span></span>

```csharp
[Key]
public int InstructorID { get; set; }
```

<span data-ttu-id="af694-235">根據預設，EF 核心視為金鑰非產生資料庫因為資料行是識別的關聯性。</span><span class="sxs-lookup"><span data-stu-id="af694-235">By default, EF Core treats the key as non-database-generated because the column is for an identifying relationship.</span></span>

### <a name="the-instructor-navigation-property"></a><span data-ttu-id="af694-236">講師導覽屬性</span><span class="sxs-lookup"><span data-stu-id="af694-236">The Instructor navigation property</span></span>

<span data-ttu-id="af694-237">`OfficeAssignment`瀏覽屬性`Instructor`可為 null 的實體，是因為：</span><span class="sxs-lookup"><span data-stu-id="af694-237">The `OfficeAssignment` navigation property for the `Instructor` entity is nullable because:</span></span>

* <span data-ttu-id="af694-238">參考類型 （例如類別是可為 null）。</span><span class="sxs-lookup"><span data-stu-id="af694-238">Reference types (such as classes are nullable).</span></span>
* <span data-ttu-id="af694-239">講師可能沒有 office 指派。</span><span class="sxs-lookup"><span data-stu-id="af694-239">An instructor might not have an office assignment.</span></span>


<span data-ttu-id="af694-240">`OfficeAssignment`實體具有不可為 null`Instructor`導覽屬性因為：</span><span class="sxs-lookup"><span data-stu-id="af694-240">The `OfficeAssignment` entity has a non-nullable `Instructor` navigation property because:</span></span>

* <span data-ttu-id="af694-241">`InstructorID`是不可為 null。</span><span class="sxs-lookup"><span data-stu-id="af694-241">`InstructorID` is non-nullable.</span></span>
* <span data-ttu-id="af694-242">沒有講師就無法存在 office 指派。</span><span class="sxs-lookup"><span data-stu-id="af694-242">An office assignment can't exist without an instructor.</span></span>

<span data-ttu-id="af694-243">當`Instructor`實體具有相關`OfficeAssignment`實體，每個實體有另一個在其導覽屬性的參考。</span><span class="sxs-lookup"><span data-stu-id="af694-243">When an `Instructor` entity has a related `OfficeAssignment` entity, each entity has a reference to the other one in its navigation property.</span></span>

<span data-ttu-id="af694-244">`[Required]`屬性無法套用至`Instructor`導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="af694-244">The `[Required]` attribute could be applied to the `Instructor` navigation property:</span></span>

```csharp
[Required]
public Instructor Instructor { get; set; }
```

<span data-ttu-id="af694-245">上述程式碼會指定必須相關的講師。</span><span class="sxs-lookup"><span data-stu-id="af694-245">The preceding code specifies that there must be a related instructor.</span></span> <span data-ttu-id="af694-246">上述程式碼不需要因為`InstructorID`（這也是在 PK） 的外部索引鍵是不可為 null。</span><span class="sxs-lookup"><span data-stu-id="af694-246">The preceding code is unnecessary because the `InstructorID` foreign key (which is also the PK) is non-nullable.</span></span>

## <a name="modify-the-course-entity"></a><span data-ttu-id="af694-247">修改課程實體</span><span class="sxs-lookup"><span data-stu-id="af694-247">Modify the Course Entity</span></span>

![課程實體](complex-data-model/_static/course-entity.png)

<span data-ttu-id="af694-249">更新*Models/Course.cs*為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="af694-249">Update *Models/Course.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Final&highlight=2,10,13,16,19,21,23)]

<span data-ttu-id="af694-250">`Course`實體具有外部索引鍵 (FK) 屬性`DepartmentID`。</span><span class="sxs-lookup"><span data-stu-id="af694-250">The `Course` entity has a foreign key (FK) property `DepartmentID`.</span></span> <span data-ttu-id="af694-251">`DepartmentID`指向 相關`Department`實體。</span><span class="sxs-lookup"><span data-stu-id="af694-251">`DepartmentID` points to the related `Department` entity.</span></span> <span data-ttu-id="af694-252">`Course`實體具有`Department`導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="af694-252">The `Course` entity has a `Department` navigation property.</span></span>

<span data-ttu-id="af694-253">EF 核心在模型具有相關實體的導覽屬性時，不需要 FK 屬性的資料模型。</span><span class="sxs-lookup"><span data-stu-id="af694-253">EF Core doesn't require a FK property for a data model when the model has a navigation property for a related entity.</span></span>

<span data-ttu-id="af694-254">在需要時會 EF 核心會自動在資料庫中建立 FKs。</span><span class="sxs-lookup"><span data-stu-id="af694-254">EF Core automatically creates FKs in the database wherever they are needed.</span></span> <span data-ttu-id="af694-255">建立 EF 核心[遮蔽屬性](https://docs.microsoft.com/ef/core/modeling/shadow-properties)FKs 自動建立的。</span><span class="sxs-lookup"><span data-stu-id="af694-255">EF Core creates [shadow properties](https://docs.microsoft.com/ef/core/modeling/shadow-properties) for automatically created FKs.</span></span> <span data-ttu-id="af694-256">在資料模型中具有 FK 可以進行更新，更簡單且更有效率。</span><span class="sxs-lookup"><span data-stu-id="af694-256">Having the FK in the data model can make updates simpler and more efficient.</span></span> <span data-ttu-id="af694-257">例如，假設模型其中 FK 屬性`DepartmentID`是*不*包含。</span><span class="sxs-lookup"><span data-stu-id="af694-257">For example, consider a model where the FK property `DepartmentID` is *not* included.</span></span> <span data-ttu-id="af694-258">當課程實體會擷取編輯：</span><span class="sxs-lookup"><span data-stu-id="af694-258">When a course entity is fetched to edit:</span></span>

* <span data-ttu-id="af694-259">`Department`實體為 null，如果未明確載入。</span><span class="sxs-lookup"><span data-stu-id="af694-259">The `Department` entity is null if it's not explicitly loaded.</span></span>
* <span data-ttu-id="af694-260">若要更新，在課程實體`Department`必須先擷取實體。</span><span class="sxs-lookup"><span data-stu-id="af694-260">To update the course entity, the `Department` entity must first be fetched.</span></span>

<span data-ttu-id="af694-261">當 FK 屬性`DepartmentID`是否包含在資料模型中，就不必再擷取`Department`之前更新的實體。</span><span class="sxs-lookup"><span data-stu-id="af694-261">When the FK property `DepartmentID` is included in the data model, there is no need to fetch the `Department` entity before an update.</span></span>

### <a name="the-databasegenerated-attribute"></a><span data-ttu-id="af694-262">DatabaseGenerated 屬性</span><span class="sxs-lookup"><span data-stu-id="af694-262">The DatabaseGenerated attribute</span></span>

<span data-ttu-id="af694-263">`[DatabaseGenerated(DatabaseGeneratedOption.None)]`屬性指定 PK 是應用程式提供，而不是產生的資料庫。</span><span class="sxs-lookup"><span data-stu-id="af694-263">The `[DatabaseGenerated(DatabaseGeneratedOption.None)]` attribute specifies that the PK is provided by the application rather than generated by the database.</span></span>

```csharp
[DatabaseGenerated(DatabaseGeneratedOption.None)]
[Display(Name = "Number")]
public int CourseID { get; set; }
```

<span data-ttu-id="af694-264">根據預設，EF 核心假設 PK 值由資料庫產生。</span><span class="sxs-lookup"><span data-stu-id="af694-264">By default, EF Core assumes that PK values are generated by the DB.</span></span> <span data-ttu-id="af694-265">DB 產生 PK 值通常是最好的方法。</span><span class="sxs-lookup"><span data-stu-id="af694-265">DB generated PK values is generally the best approach.</span></span> <span data-ttu-id="af694-266">如`Course`實體，使用者指定 PK</span><span class="sxs-lookup"><span data-stu-id="af694-266">For `Course` entities, the user specifies the PK.</span></span> <span data-ttu-id="af694-267">例如，課程號碼例如 1000年一連串數學部門、 2000年一連串的英文版的部門。</span><span class="sxs-lookup"><span data-stu-id="af694-267">For example, a course number such as a 1000 series for the math department, a 2000 series for the English department.</span></span>

<span data-ttu-id="af694-268">`DatabaseGenerated`屬性也可以用來產生預設值。</span><span class="sxs-lookup"><span data-stu-id="af694-268">The `DatabaseGenerated` attribute can also be used to generate default values.</span></span> <span data-ttu-id="af694-269">例如，資料庫可以自動產生日期欄位來記錄資料列已建立或更新的日期。</span><span class="sxs-lookup"><span data-stu-id="af694-269">For example, the DB can automatically generate a date field to record the date a row was created or updated.</span></span> <span data-ttu-id="af694-270">如需詳細資訊，請參閱[產生屬性](https://docs.microsoft.com/ef/core/modeling/generated-properties)。</span><span class="sxs-lookup"><span data-stu-id="af694-270">For more information, see [Generated Properties](https://docs.microsoft.com/ef/core/modeling/generated-properties).</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="af694-271">外部索引鍵和導覽屬性</span><span class="sxs-lookup"><span data-stu-id="af694-271">Foreign key and navigation properties</span></span>

<span data-ttu-id="af694-272">外部索引鍵 (FK) 屬性和導覽屬性中的`Course`實體反映的下列關聯性：</span><span class="sxs-lookup"><span data-stu-id="af694-272">The foreign key (FK) properties and navigation properties in the `Course` entity reflect the following relationships:</span></span>

<span data-ttu-id="af694-273">課程指派給一個部門，所以`DepartmentID`FK 和`Department`導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="af694-273">A course is assigned to one department, so there's a `DepartmentID` FK and a `Department` navigation property.</span></span>

```csharp
public int DepartmentID { get; set; }
public Department Department { get; set; }
```

<span data-ttu-id="af694-274">課程可以有任意數目的學生註冊，所以`Enrollments`導覽屬性是集合：</span><span class="sxs-lookup"><span data-stu-id="af694-274">A course can have any number of students enrolled in it, so the `Enrollments` navigation property is a collection:</span></span>

```csharp
public ICollection<Enrollment> Enrollments { get; set; }
```

<span data-ttu-id="af694-275">課程會教由多個講師，所以`CourseAssignments`導覽屬性是集合：</span><span class="sxs-lookup"><span data-stu-id="af694-275">A course may be taught by multiple instructors, so the `CourseAssignments` navigation property is a collection:</span></span>

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

<span data-ttu-id="af694-276">`CourseAssignment`說明[稍後](#many-to-many-relationships)。</span><span class="sxs-lookup"><span data-stu-id="af694-276">`CourseAssignment` is explained [later](#many-to-many-relationships).</span></span>

## <a name="create-the-department-entity"></a><span data-ttu-id="af694-277">建立 Department 實體</span><span class="sxs-lookup"><span data-stu-id="af694-277">Create the Department entity</span></span>

![Department 實體](complex-data-model/_static/department-entity.png)

<span data-ttu-id="af694-279">建立*Models/Department.cs*為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="af694-279">Create *Models/Department.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Department.cs?name=snippet_Begin)]

### <a name="the-column-attribute"></a><span data-ttu-id="af694-280">資料行屬性</span><span class="sxs-lookup"><span data-stu-id="af694-280">The Column attribute</span></span>

<span data-ttu-id="af694-281">先前`Column`屬性用來變更資料行名稱的對應。</span><span class="sxs-lookup"><span data-stu-id="af694-281">Previously the `Column` attribute was used to change column name mapping.</span></span> <span data-ttu-id="af694-282">在程式碼`Department`實體，`Column`屬性用來變更 SQL 資料類型對應。</span><span class="sxs-lookup"><span data-stu-id="af694-282">In the code for the `Department` entity, the `Column` attribute is used to change SQL data type mapping.</span></span> <span data-ttu-id="af694-283">`Budget` DB 中使用 SQL Server money 類型來定義資料行：</span><span class="sxs-lookup"><span data-stu-id="af694-283">The `Budget` column is defined using the SQL Server money type in the DB:</span></span>

```csharp
[Column(TypeName="money")]
public decimal Budget { get; set; }
```

<span data-ttu-id="af694-284">資料行對應則通常不需要。</span><span class="sxs-lookup"><span data-stu-id="af694-284">Column mapping is generally not required.</span></span> <span data-ttu-id="af694-285">EF 核心通常會選擇適當屬性的 CLR 型別為基礎的 SQL Server 資料型別。</span><span class="sxs-lookup"><span data-stu-id="af694-285">EF Core generally chooses the appropriate SQL Server data type based on the CLR type for the property.</span></span> <span data-ttu-id="af694-286">CLR`decimal`類型會對應至 SQL Server`decimal`型別。</span><span class="sxs-lookup"><span data-stu-id="af694-286">The CLR `decimal` type maps to a SQL Server `decimal` type.</span></span> <span data-ttu-id="af694-287">`Budget`適用於貨幣和 money 資料類型為更適當的貨幣。</span><span class="sxs-lookup"><span data-stu-id="af694-287">`Budget` is for currency, and the money data type is more appropriate for currency.</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="af694-288">外部索引鍵和導覽屬性</span><span class="sxs-lookup"><span data-stu-id="af694-288">Foreign key and navigation properties</span></span>

<span data-ttu-id="af694-289">FK 和導覽屬性會反映的下列關聯性：</span><span class="sxs-lookup"><span data-stu-id="af694-289">The FK and navigation properties reflect the following relationships:</span></span>

* <span data-ttu-id="af694-290">部門可能會或可能沒有系統管理員。</span><span class="sxs-lookup"><span data-stu-id="af694-290">A department may or may not have an administrator.</span></span>
* <span data-ttu-id="af694-291">系統管理員永遠是講師。</span><span class="sxs-lookup"><span data-stu-id="af694-291">An administrator is always an instructor.</span></span> <span data-ttu-id="af694-292">因此`InstructorID`屬性做為包含要 FK`Instructor`實體。</span><span class="sxs-lookup"><span data-stu-id="af694-292">Therefore the `InstructorID` property is included as the FK to the `Instructor` entity.</span></span>

<span data-ttu-id="af694-293">導覽屬性名為`Administrator`但保留`Instructor`實體：</span><span class="sxs-lookup"><span data-stu-id="af694-293">The navigation property is named `Administrator` but holds an `Instructor` entity:</span></span>

```csharp
public int? InstructorID { get; set; }
public Instructor Administrator { get; set; }
```

<span data-ttu-id="af694-294">問號 （？），在上述程式碼中指定的屬性是可為 null。</span><span class="sxs-lookup"><span data-stu-id="af694-294">The question mark (?) in the preceding code specifies the property is nullable.</span></span>

<span data-ttu-id="af694-295">部門可能具有許多課程，課程導覽屬性是：</span><span class="sxs-lookup"><span data-stu-id="af694-295">A department may have many courses, so there's a Courses navigation property:</span></span>

```csharp
public ICollection<Course> Courses { get; set; }
```

<span data-ttu-id="af694-296">注意： 依照慣例，EF 核心 可讓 cascade delete 不可為 null 的 FKs 和多對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="af694-296">Note: By convention, EF Core enables cascade delete for non-nullable FKs and for many-to-many relationships.</span></span> <span data-ttu-id="af694-297">串聯刪除可能會導致循環的串聯刪除規則。</span><span class="sxs-lookup"><span data-stu-id="af694-297">Cascading delete can result in circular cascade delete rules.</span></span> <span data-ttu-id="af694-298">循環的 cascade 加入移轉時，刪除規則原因例外狀況。</span><span class="sxs-lookup"><span data-stu-id="af694-298">Circular cascade delete rules causes an exception when a migration is added.</span></span>

<span data-ttu-id="af694-299">例如，如果`Department.InstructorID`屬性未定義為可為 null:</span><span class="sxs-lookup"><span data-stu-id="af694-299">For example, if the `Department.InstructorID` property was not defined as nullable:</span></span>

* <span data-ttu-id="af694-300">EF 核心設定部門刪除時刪除講師串聯刪除規則。</span><span class="sxs-lookup"><span data-stu-id="af694-300">EF Core configures a cascade delete rule to delete the instructor when the department is deleted.</span></span>
* <span data-ttu-id="af694-301">刪除講師部門刪除時，不是預期的行為。</span><span class="sxs-lookup"><span data-stu-id="af694-301">Deleting the instructor when the department is deleted is not the intended behavior.</span></span>

<span data-ttu-id="af694-302">如果需要使用商務規則`InstructorID`屬性都不可為 null，使用下列 fluent API 陳述式：</span><span class="sxs-lookup"><span data-stu-id="af694-302">If business rules required the `InstructorID` property be non-nullable, use the following fluent API statement:</span></span>

 ```csharp
 modelBuilder.Entity<Department>()
    .HasOne(d => d.Administrator)
    .WithMany()
    .OnDelete(DeleteBehavior.Restrict)
 ```

<span data-ttu-id="af694-303">上述程式碼會停用 cascade delete 部門講師關聯性。</span><span class="sxs-lookup"><span data-stu-id="af694-303">The preceding code disables cascade delete on the department-instructor relationship.</span></span>

## <a name="update-the-enrollment-entity"></a><span data-ttu-id="af694-304">更新註冊實體</span><span class="sxs-lookup"><span data-stu-id="af694-304">Update the Enrollment entity</span></span>

<span data-ttu-id="af694-305">註冊記錄是由一位學生採取一個課程。</span><span class="sxs-lookup"><span data-stu-id="af694-305">An enrollment record is for a one course taken by one student.</span></span>

![註冊實體](complex-data-model/_static/enrollment-entity.png)

<span data-ttu-id="af694-307">更新*Models/Enrollment.cs*為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="af694-307">Update *Models/Enrollment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Final&highlight=1-2,16)]

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="af694-308">外部索引鍵和導覽屬性</span><span class="sxs-lookup"><span data-stu-id="af694-308">Foreign key and navigation properties</span></span>

<span data-ttu-id="af694-309">FK 屬性和導覽屬性會反映下列關聯性：</span><span class="sxs-lookup"><span data-stu-id="af694-309">The FK properties and navigation properties reflect the following relationships:</span></span>

<span data-ttu-id="af694-310">註冊記錄是一個課程中，所以沒有`CourseID`FK 屬性和`Course`導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="af694-310">An enrollment record is for one course, so there's a `CourseID` FK property and a `Course` navigation property:</span></span>

```csharp
public int CourseID { get; set; }
public Course Course { get; set; }
```

<span data-ttu-id="af694-311">註冊記錄是一個學生，所以沒有`StudentID`FK 屬性和`Student`導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="af694-311">An enrollment record is for one student, so there's a `StudentID` FK property and a `Student` navigation property:</span></span>

```csharp
public int StudentID { get; set; }
public Student Student { get; set; }
```

## <a name="many-to-many-relationships"></a><span data-ttu-id="af694-312">多對多關聯性</span><span class="sxs-lookup"><span data-stu-id="af694-312">Many-to-Many Relationships</span></span>

<span data-ttu-id="af694-313">多對多關聯性之間`Student`和`Course`實體。</span><span class="sxs-lookup"><span data-stu-id="af694-313">There's a many-to-many relationship between the `Student` and `Course` entities.</span></span> <span data-ttu-id="af694-314">`Enrollment`實體做為多對多聯結資料表*裝載*資料庫中。</span><span class="sxs-lookup"><span data-stu-id="af694-314">The `Enrollment` entity functions as a many-to-many join table *with payload* in the database.</span></span> <span data-ttu-id="af694-315">「 裝載 」 表示`Enrollment`資料表包含額外資料除了 FKs 聯結的資料表 (在此情況下，在 PK 和`Grade`)。</span><span class="sxs-lookup"><span data-stu-id="af694-315">"With payload" means that the `Enrollment` table contains additional data besides FKs for the joined tables (in this case, the PK and `Grade`).</span></span>

<span data-ttu-id="af694-316">下圖顯示這些關聯性中的實體圖表的外觀。</span><span class="sxs-lookup"><span data-stu-id="af694-316">The following illustration shows what these relationships look like in an entity diagram.</span></span> <span data-ttu-id="af694-317">(此圖表使用產生的 EF Power Tools 的 EF 6.x。</span><span class="sxs-lookup"><span data-stu-id="af694-317">(This diagram was generated using EF Power Tools for EF 6.x.</span></span> <span data-ttu-id="af694-318">建立圖表不是本教學課程的一部分。）</span><span class="sxs-lookup"><span data-stu-id="af694-318">Creating the diagram isn't part of the tutorial.)</span></span>

![學生課程多對多關聯性](complex-data-model/_static/student-course.png)

<span data-ttu-id="af694-320">每個關聯性線條在另一個對多關聯性，表示有一個結束作業，並以星號 （*） 1。</span><span class="sxs-lookup"><span data-stu-id="af694-320">Each relationship line has a 1 at one end and an asterisk (*) at the other, indicating a one-to-many relationship.</span></span>

<span data-ttu-id="af694-321">如果`Enrollment`資料表未包含等級資訊，它只需要包含兩個 FKs (`CourseID`和`StudentID`)。</span><span class="sxs-lookup"><span data-stu-id="af694-321">If the `Enrollment` table didn't include grade information, it would only need to contain the two FKs (`CourseID` and `StudentID`).</span></span> <span data-ttu-id="af694-322">多對多聯結資料表沒有裝載有時稱為純聯結資料表 (PJT)。</span><span class="sxs-lookup"><span data-stu-id="af694-322">A many-to-many join table without payload is sometimes called a pure join table (PJT).</span></span>

<span data-ttu-id="af694-323">`Instructor`和`Course`實體具有使用純聯結資料表的多對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="af694-323">The `Instructor` and `Course` entities have a many-to-many relationship using a pure join table.</span></span>

<span data-ttu-id="af694-324">注意： EF 6.x 支援多對多關聯性，但 EF 核心隱含聯結資料表並不會。</span><span class="sxs-lookup"><span data-stu-id="af694-324">Note: EF 6.x supports implicit join tables for many-to-many relationships, but EF Core does not.</span></span> <span data-ttu-id="af694-325">如需詳細資訊，請參閱[多對多關聯性在 EF 核心 2.0](https://blog.oneunicorn.com/2017/09/25/many-to-many-relationships-in-ef-core-2-0-part-1-the-basics/)。</span><span class="sxs-lookup"><span data-stu-id="af694-325">For more information, see [Many-to-many relationships in EF Core 2.0](https://blog.oneunicorn.com/2017/09/25/many-to-many-relationships-in-ef-core-2-0-part-1-the-basics/).</span></span>

## <a name="the-courseassignment-entity"></a><span data-ttu-id="af694-326">CourseAssignment 實體</span><span class="sxs-lookup"><span data-stu-id="af694-326">The CourseAssignment entity</span></span>

![CourseAssignment 實體](complex-data-model/_static/courseassignment-entity.png)

<span data-ttu-id="af694-328">建立*Models/CourseAssignment.cs*為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="af694-328">Create *Models/CourseAssignment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/CourseAssignment.cs)]

### <a name="instructor-to-courses"></a><span data-ttu-id="af694-329">講師-課程</span><span class="sxs-lookup"><span data-stu-id="af694-329">Instructor-to-Courses</span></span>

![講師-課程 m:M](complex-data-model/_static/courseassignment.png)

<span data-ttu-id="af694-331">講師-課程多對多關聯性：</span><span class="sxs-lookup"><span data-stu-id="af694-331">The Instructor-to-Courses many-to-many relationship:</span></span>

* <span data-ttu-id="af694-332">需要聯結資料表，必須由實體集。</span><span class="sxs-lookup"><span data-stu-id="af694-332">Requires a join table that must be represented by an entity set.</span></span>
* <span data-ttu-id="af694-333">是一個純聯結資料表 （沒有內容的資料表）。</span><span class="sxs-lookup"><span data-stu-id="af694-333">Is a pure join table (table without payload).</span></span>

<span data-ttu-id="af694-334">通常會命名為聯結實體`EntityName1EntityName2`。</span><span class="sxs-lookup"><span data-stu-id="af694-334">It's common to name a join entity `EntityName1EntityName2`.</span></span> <span data-ttu-id="af694-335">例如，使用這個模式對講師-課程聯結資料表是`CourseInstructor`。</span><span class="sxs-lookup"><span data-stu-id="af694-335">For example, the Instructor-to-Courses join table using this pattern is `CourseInstructor`.</span></span> <span data-ttu-id="af694-336">不過，我們建議使用可描述關聯性的名稱。</span><span class="sxs-lookup"><span data-stu-id="af694-336">However, we recommend using a name that describes the relationship.</span></span>

<span data-ttu-id="af694-337">資料模型開始簡單及成長。</span><span class="sxs-lookup"><span data-stu-id="af694-337">Data models start out simple and grow.</span></span> <span data-ttu-id="af694-338">要包含裝載經常發展否裝載聯結 (PJTs)。</span><span class="sxs-lookup"><span data-stu-id="af694-338">No-payload joins (PJTs) frequently evolve to include payload.</span></span> <span data-ttu-id="af694-339">藉由啟動具有描述性的實體名稱，名稱不需要變更聯結資料表時變更。</span><span class="sxs-lookup"><span data-stu-id="af694-339">By starting with a descriptive entity name, the name doesn't need to change when the join table changes.</span></span> <span data-ttu-id="af694-340">理想情況下，聯結實體商務網域中必須有自己的自然 (可能是單一 word) 名稱。</span><span class="sxs-lookup"><span data-stu-id="af694-340">Ideally, the join entity would have its own natural (possibly single word) name in the business domain.</span></span> <span data-ttu-id="af694-341">例如，書籍客戶無法連結與聯結實體稱為評等。</span><span class="sxs-lookup"><span data-stu-id="af694-341">For example, Books and Customers could be linked with a join entity called Ratings.</span></span> <span data-ttu-id="af694-342">講師-課程多對多關聯性，`CourseAssignment`最好透過`CourseInstructor`。</span><span class="sxs-lookup"><span data-stu-id="af694-342">For the Instructor-to-Courses many-to-many relationship, `CourseAssignment` is preferred over `CourseInstructor`.</span></span>

### <a name="composite-key"></a><span data-ttu-id="af694-343">複合索引鍵</span><span class="sxs-lookup"><span data-stu-id="af694-343">Composite key</span></span>

<span data-ttu-id="af694-344">FKs 不是可為 null。</span><span class="sxs-lookup"><span data-stu-id="af694-344">FKs are not nullable.</span></span> <span data-ttu-id="af694-345">在兩個 FKs `CourseAssignment` (`InstructorID`和`CourseID`) 一起唯一識別每個資料列的`CourseAssignment`資料表。</span><span class="sxs-lookup"><span data-stu-id="af694-345">The two FKs in `CourseAssignment` (`InstructorID` and `CourseID`) together uniquely identify each row of the `CourseAssignment` table.</span></span> <span data-ttu-id="af694-346">`CourseAssignment`不需要專用的 PK</span><span class="sxs-lookup"><span data-stu-id="af694-346">`CourseAssignment` doesn't require a dedicated PK.</span></span> <span data-ttu-id="af694-347">`InstructorID`和`CourseID`屬性當做複合 PK</span><span class="sxs-lookup"><span data-stu-id="af694-347">The `InstructorID` and `CourseID` properties function as a composite PK.</span></span> <span data-ttu-id="af694-348">若要指定複合 PKs 到 EF Core 的唯一方法是使用*fluent API*。</span><span class="sxs-lookup"><span data-stu-id="af694-348">The only way to specify composite PKs to EF Core is with the *fluent API*.</span></span> <span data-ttu-id="af694-349">下節會說明如何設定複合 PK</span><span class="sxs-lookup"><span data-stu-id="af694-349">The next section shows how to configure the composite PK.</span></span>

<span data-ttu-id="af694-350">複合索引鍵，以確保：</span><span class="sxs-lookup"><span data-stu-id="af694-350">The composite key ensures:</span></span>

* <span data-ttu-id="af694-351">一個課程允許多個資料列。</span><span class="sxs-lookup"><span data-stu-id="af694-351">Multiple rows are allowed for one course.</span></span>
* <span data-ttu-id="af694-352">一個講師允許多個資料列。</span><span class="sxs-lookup"><span data-stu-id="af694-352">Multiple rows are allowed for one instructor.</span></span>
* <span data-ttu-id="af694-353">不允許多個資料列的相同講師和課程。</span><span class="sxs-lookup"><span data-stu-id="af694-353">Multiple rows for the same instructor and course is not allowed.</span></span>

<span data-ttu-id="af694-354">`Enrollment`聯結實體定義自己的 PK，因此可能會有這種重複的項目。</span><span class="sxs-lookup"><span data-stu-id="af694-354">The `Enrollment` join entity defines its own PK, so duplicates of this sort are possible.</span></span> <span data-ttu-id="af694-355">若要防止這類重複項目：</span><span class="sxs-lookup"><span data-stu-id="af694-355">To prevent such duplicates:</span></span>

* <span data-ttu-id="af694-356">FK 欄位上加入唯一索引或</span><span class="sxs-lookup"><span data-stu-id="af694-356">Add a unique index on the FK fields, or</span></span>
* <span data-ttu-id="af694-357">設定`Enrollment`主複合索引鍵類似`CourseAssignment`。</span><span class="sxs-lookup"><span data-stu-id="af694-357">Configure `Enrollment` with a primary composite key similar to `CourseAssignment`.</span></span> <span data-ttu-id="af694-358">如需詳細資訊，請參閱[索引](https://docs.microsoft.com/ef/core/modeling/indexes)。</span><span class="sxs-lookup"><span data-stu-id="af694-358">For more information, see [Indexes](https://docs.microsoft.com/ef/core/modeling/indexes).</span></span>

## <a name="update-the-db-context"></a><span data-ttu-id="af694-359">更新 DB 內容</span><span class="sxs-lookup"><span data-stu-id="af694-359">Update the DB context</span></span>

<span data-ttu-id="af694-360">將下列反白顯示的程式碼加入*Data/SchoolContext.cs*:</span><span class="sxs-lookup"><span data-stu-id="af694-360">Add the following highlighted code to *Data/SchoolContext.cs*:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_BeforeInheritance&highlight=15-18,25-31)]

<span data-ttu-id="af694-361">上述程式碼會新增新的實體，並設定`CourseAssignment`實體的複合 PK</span><span class="sxs-lookup"><span data-stu-id="af694-361">The preceding code adds the new entities and configures the `CourseAssignment` entity's composite PK.</span></span>

## <a name="fluent-api-alternative-to-attributes"></a><span data-ttu-id="af694-362">Fluent API 替代項目屬性</span><span class="sxs-lookup"><span data-stu-id="af694-362">Fluent API alternative to attributes</span></span>

<span data-ttu-id="af694-363">`OnModelCreating`方法，在上述程式碼會使用*fluent API*設定 EF 核心行為。</span><span class="sxs-lookup"><span data-stu-id="af694-363">The `OnModelCreating` method in the preceding code uses the *fluent API* to configure EF Core behavior.</span></span> <span data-ttu-id="af694-364">API 稱為 「 fluent 應用程式開發，因為它通常由串連一系列的方法呼叫一起成單一陳述式。</span><span class="sxs-lookup"><span data-stu-id="af694-364">The API is called "fluent" because it's often used by stringing a series of method calls together into a single statement.</span></span> <span data-ttu-id="af694-365">[下列程式碼](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration)是 fluent 應用程式開發的應用程式開發介面的範例：</span><span class="sxs-lookup"><span data-stu-id="af694-365">The [following code](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration) is an example of the fluent API:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Url)
        .IsRequired();
}
```

<span data-ttu-id="af694-366">在本教學課程，fluent 應用程式開發的應用程式開發介面只適用於無法透過屬性的 DB 對應。</span><span class="sxs-lookup"><span data-stu-id="af694-366">In this tutorial, the fluent API is used only for DB mapping that can't be done with attributes.</span></span> <span data-ttu-id="af694-367">不過，fluent 應用程式開發的應用程式開發介面，可以指定大部分的格式設定、 驗證和對應規則，可以使用屬性。</span><span class="sxs-lookup"><span data-stu-id="af694-367">However, the fluent API can specify most of the formatting, validation, and mapping rules that can be done with attributes.</span></span>

<span data-ttu-id="af694-368">某些屬性，例如`MinimumLength`fluent 應用程式開發的應用程式開發介面無法套用。</span><span class="sxs-lookup"><span data-stu-id="af694-368">Some attributes such as `MinimumLength` can't be applied with the fluent API.</span></span> <span data-ttu-id="af694-369">`MinimumLength`不會變更結構描述中，它只適用於最小長度驗證規則。</span><span class="sxs-lookup"><span data-stu-id="af694-369">`MinimumLength` doesn't change the schema, it only applies a minimum length validation rule.</span></span>

<span data-ttu-id="af694-370">有些開發人員偏好使用 fluent 應用程式開發的應用程式開發介面，以獨佔方式，讓它們可保留他們的實體類別 「 清除 」。</span><span class="sxs-lookup"><span data-stu-id="af694-370">Some developers prefer to use the fluent API exclusively so that they can keep their entity classes "clean."</span></span> <span data-ttu-id="af694-371">可以混合屬性和 fluent 應用程式開發的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="af694-371">Attributes and the fluent API can be mixed.</span></span> <span data-ttu-id="af694-372">有一些設定，才可使用 fluent API （指定複合 PK）。</span><span class="sxs-lookup"><span data-stu-id="af694-372">There are some configurations that can only be done with the fluent API (specifying a composite PK).</span></span> <span data-ttu-id="af694-373">有某些只能透過屬性的組態 (`MinimumLength`)。</span><span class="sxs-lookup"><span data-stu-id="af694-373">There are some configurations that can only be done with attributes (`MinimumLength`).</span></span> <span data-ttu-id="af694-374">使用 fluent 應用程式開發的應用程式開發介面或屬性的建議的做法：</span><span class="sxs-lookup"><span data-stu-id="af694-374">The recommended practice for using fluent API or attributes:</span></span>

* <span data-ttu-id="af694-375">選擇其中一個這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="af694-375">Choose one of these two approaches.</span></span>
* <span data-ttu-id="af694-376">使用一致的方式盡量所選擇的方法。</span><span class="sxs-lookup"><span data-stu-id="af694-376">Use the chosen approach consistently as much as possible.</span></span>

<span data-ttu-id="af694-377">有些用於這個屬性會用於教學課程：</span><span class="sxs-lookup"><span data-stu-id="af694-377">Some of the attributes used in the this tutorial are used for:</span></span>

* <span data-ttu-id="af694-378">驗證 (例如， `MinimumLength`)。</span><span class="sxs-lookup"><span data-stu-id="af694-378">Validation only (for example, `MinimumLength`).</span></span>
* <span data-ttu-id="af694-379">只有 EF 核心設定 (例如， `HasKey`)。</span><span class="sxs-lookup"><span data-stu-id="af694-379">EF Core configuration only (for example, `HasKey`).</span></span>
* <span data-ttu-id="af694-380">驗證和 EF 核心設定 (例如， `[StringLength(50)]`)。</span><span class="sxs-lookup"><span data-stu-id="af694-380">Validation and EF Core configuration (for example, `[StringLength(50)]`).</span></span>

<span data-ttu-id="af694-381">如需 fluent API 與屬性的詳細資訊，請參閱[的組態方法](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration)。</span><span class="sxs-lookup"><span data-stu-id="af694-381">For more information about attributes vs. fluent API, see [Methods of configuration](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration).</span></span>

## <a name="entity-diagram-showing-relationships"></a><span data-ttu-id="af694-382">實體圖表顯示關聯性</span><span class="sxs-lookup"><span data-stu-id="af694-382">Entity Diagram Showing Relationships</span></span>

<span data-ttu-id="af694-383">下圖顯示為已完成的 School 模型的 EF Power Tools 建立的圖表。</span><span class="sxs-lookup"><span data-stu-id="af694-383">The following illustration shows the diagram that EF Power Tools create for the completed School model.</span></span>

![實體圖表](complex-data-model/_static/diagram.png)

<span data-ttu-id="af694-385">在上圖顯示：</span><span class="sxs-lookup"><span data-stu-id="af694-385">The preceding diagram shows:</span></span>

* <span data-ttu-id="af694-386">數個一對多關聯性線條 (1 到\*)。</span><span class="sxs-lookup"><span data-stu-id="af694-386">Several one-to-many relationship lines (1 to \*).</span></span>
* <span data-ttu-id="af694-387">以 0 或-1 一個之間的關聯線 (1 對 0..1)`Instructor`和`OfficeAssignment`實體。</span><span class="sxs-lookup"><span data-stu-id="af694-387">The one-to-zero-or-one relationship line (1 to 0..1) between the `Instructor` and `OfficeAssignment` entities.</span></span>
* <span data-ttu-id="af694-388">零-或--一對多關聯性線條 (0..1 對 *) 之間`Instructor`和`Department`實體。</span><span class="sxs-lookup"><span data-stu-id="af694-388">The zero-or-one-to-many relationship line (0..1 to *) between the `Instructor` and `Department` entities.</span></span>

## <a name="seed-the-db-with-test-data"></a><span data-ttu-id="af694-389">種子使用的測試資料的資料庫</span><span class="sxs-lookup"><span data-stu-id="af694-389">Seed the DB with Test Data</span></span>

<span data-ttu-id="af694-390">更新中的程式碼*Data/DbInitializer.cs*:</span><span class="sxs-lookup"><span data-stu-id="af694-390">Update the code in *Data/DbInitializer.cs*:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Final)]

<span data-ttu-id="af694-391">上述程式碼會提供新的實體中的種子資料。</span><span class="sxs-lookup"><span data-stu-id="af694-391">The preceding code provides seed data for the new entities.</span></span> <span data-ttu-id="af694-392">大部分的這段程式碼會建立新的實體物件，並載入資料範例。</span><span class="sxs-lookup"><span data-stu-id="af694-392">Most of this code creates new entity objects and loads sample data.</span></span> <span data-ttu-id="af694-393">範例資料用於測試。</span><span class="sxs-lookup"><span data-stu-id="af694-393">The sample data is used for testing.</span></span> <span data-ttu-id="af694-394">上述程式碼會建立下列的多對多關聯性：</span><span class="sxs-lookup"><span data-stu-id="af694-394">The preceding code creates the following many-to-many relationships:</span></span>

* `Enrollments`
* `CourseAssignment`

<span data-ttu-id="af694-395">注意： [EF 核心 2.1](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap)將支援[資料植入](https://github.com/aspnet/EntityFrameworkCore/issues/629)。</span><span class="sxs-lookup"><span data-stu-id="af694-395">Note: [EF Core 2.1](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap) will support [data seeding](https://github.com/aspnet/EntityFrameworkCore/issues/629).</span></span>

## <a name="add-a-migration"></a><span data-ttu-id="af694-396">新增移轉</span><span class="sxs-lookup"><span data-stu-id="af694-396">Add a migration</span></span>

<span data-ttu-id="af694-397">建置專案。</span><span class="sxs-lookup"><span data-stu-id="af694-397">Build the project.</span></span> <span data-ttu-id="af694-398">專案資料夾中開啟命令視窗並輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="af694-398">Open a command window in the project folder and enter the following command:</span></span>

```console
dotnet ef migrations add ComplexDataModel
```

<span data-ttu-id="af694-399">上述命令會顯示有關可能遺失資料的警告。</span><span class="sxs-lookup"><span data-stu-id="af694-399">The preceding command displays a warning about possible data loss.</span></span>

```text
An operation was scaffolded that may result in the loss of data.
Please review the migration for accuracy.
Done. To undo this action, use 'ef migrations remove'
```

<span data-ttu-id="af694-400">如果`database update`執行命令時，會產生下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="af694-400">If the `database update` command is run, the following error is produced:</span></span>

```text
The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK_dbo.Course_dbo.Department_DepartmentID". The conflict occurred in
database "ContosoUniversity", table "dbo.Department", column 'DepartmentID'.
```

<span data-ttu-id="af694-401">移轉作業執行時使用現有的資料，可能有不滿意的現有資料的 FK 條件約束。</span><span class="sxs-lookup"><span data-stu-id="af694-401">When migrations are run with existing data, there may be FK constraints that are not satisfied with the exiting data.</span></span> <span data-ttu-id="af694-402">此教學課程中，會建立新的資料庫，因此沒有 FK 條件約束違規。</span><span class="sxs-lookup"><span data-stu-id="af694-402">For this tutorial, a new DB is created, so there are no FK constraint violations.</span></span> <span data-ttu-id="af694-403">請參閱[修正 foreign key 條件約束與傳統資料](#fk)如需如何在目前的 DB 修正 FK 違規的指示。</span><span class="sxs-lookup"><span data-stu-id="af694-403">See [Fixing foreign key constraints with legacy data](#fk) for instructions on how to fix the FK violations on the current DB.</span></span>

## <a name="change-the-connection-string-and-update-the-db"></a><span data-ttu-id="af694-404">變更連接字串，並更新資料庫</span><span class="sxs-lookup"><span data-stu-id="af694-404">Change the connection string and update the DB</span></span>

<span data-ttu-id="af694-405">中已更新的程式碼`DbInitializer`加入新的實體的種子資料。</span><span class="sxs-lookup"><span data-stu-id="af694-405">The code in the updated `DbInitializer` adds seed data for the new entities.</span></span> <span data-ttu-id="af694-406">若要強制建立新的空白資料庫的 EF 核心：</span><span class="sxs-lookup"><span data-stu-id="af694-406">To force EF Core to create a new empty DB:</span></span>

* <span data-ttu-id="af694-407">資料庫連接字串中變更名稱*appsettings.json* ContosoUniversity3 至。</span><span class="sxs-lookup"><span data-stu-id="af694-407">Change the DB connection string name in *appsettings.json* to ContosoUniversity3.</span></span> <span data-ttu-id="af694-408">新的名稱必須是電腦未使用的名稱。</span><span class="sxs-lookup"><span data-stu-id="af694-408">The new name must be a name that hasn't been used on the computer.</span></span>

    ```json
    {
      "ConnectionStrings": {
        "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=ContosoUniversity3;Trusted_Connection=True;MultipleActiveResultSets=true"
      },
    ```

* <span data-ttu-id="af694-409">或者，刪除資料庫的使用：</span><span class="sxs-lookup"><span data-stu-id="af694-409">Alternatively, delete the DB using:</span></span>

    * <span data-ttu-id="af694-410">**SQL Server 物件總管**(SSOX)。</span><span class="sxs-lookup"><span data-stu-id="af694-410">**SQL Server Object Explorer** (SSOX).</span></span>
    * <span data-ttu-id="af694-411">`database drop` CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="af694-411">The `database drop` CLI command:</span></span>

   ```console
   dotnet ef database drop
   ```

<span data-ttu-id="af694-412">執行`database update`命令視窗中：</span><span class="sxs-lookup"><span data-stu-id="af694-412">Run `database update` in the command window:</span></span>

```console
dotnet ef database update
```

<span data-ttu-id="af694-413">上述命令會執行所有移轉。</span><span class="sxs-lookup"><span data-stu-id="af694-413">The preceding command runs all the migrations.</span></span>

<span data-ttu-id="af694-414">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="af694-414">Run the app.</span></span> <span data-ttu-id="af694-415">執行應用程式執行`DbInitializer.Initialize`方法。</span><span class="sxs-lookup"><span data-stu-id="af694-415">Running the app runs the `DbInitializer.Initialize` method.</span></span> <span data-ttu-id="af694-416">`DbInitializer.Initialize`填入新的 DB。</span><span class="sxs-lookup"><span data-stu-id="af694-416">The `DbInitializer.Initialize` populates the new DB.</span></span>

<span data-ttu-id="af694-417">開啟 SSOX DB:</span><span class="sxs-lookup"><span data-stu-id="af694-417">Open the DB in SSOX:</span></span>

* <span data-ttu-id="af694-418">展開**資料表**節點。</span><span class="sxs-lookup"><span data-stu-id="af694-418">Expand the **Tables** node.</span></span> <span data-ttu-id="af694-419">會顯示建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="af694-419">The created tables are displayed.</span></span>
* <span data-ttu-id="af694-420">如果先前已開啟 SSOX，按一下**重新整理** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="af694-420">If SSOX was opened previously, click the **Refresh** button.</span></span>

![SSOX 中的資料表](complex-data-model/_static/ssox-tables.png)

<span data-ttu-id="af694-422">檢查**CourseAssignment**資料表：</span><span class="sxs-lookup"><span data-stu-id="af694-422">Examine the **CourseAssignment** table:</span></span>

* <span data-ttu-id="af694-423">以滑鼠右鍵按一下**CourseAssignment**資料表，然後選取**檢視資料**。</span><span class="sxs-lookup"><span data-stu-id="af694-423">Right-click the **CourseAssignment** table and select **View Data**.</span></span>
* <span data-ttu-id="af694-424">確認**CourseAssignment**資料表包含資料。</span><span class="sxs-lookup"><span data-stu-id="af694-424">Verify the **CourseAssignment** table contains data.</span></span>

![SSOX CourseAssignment 資料](complex-data-model/_static/ssox-ci-data.png)

<a name="fk"></a>

## <a name="fixing-foreign-key-constraints-with-legacy-data"></a><span data-ttu-id="af694-426">與傳統資料修正 foreign key 條件約束</span><span class="sxs-lookup"><span data-stu-id="af694-426">Fixing foreign key constraints with legacy data</span></span>

<span data-ttu-id="af694-427">此區段是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="af694-427">This section is optional.</span></span>

<span data-ttu-id="af694-428">移轉作業執行時使用現有的資料，可能有不滿意的現有資料的 FK 條件約束。</span><span class="sxs-lookup"><span data-stu-id="af694-428">When migrations are run with existing data, there may be FK constraints that are not satisfied with the exiting data.</span></span> <span data-ttu-id="af694-429">使用生產資料，必須採取步驟來移轉現有的資料。</span><span class="sxs-lookup"><span data-stu-id="af694-429">With production data, steps must be taken to migrate the existing data.</span></span> <span data-ttu-id="af694-430">本節提供修正 FK 條件約束違規的範例。</span><span class="sxs-lookup"><span data-stu-id="af694-430">This section provides an example of fixing FK constraint violations.</span></span> <span data-ttu-id="af694-431">不要變更這些程式碼不使用備份。</span><span class="sxs-lookup"><span data-stu-id="af694-431">Don't make these code changes without a backup.</span></span> <span data-ttu-id="af694-432">不要讓這些程式碼變更，如果您已完成上一節，並更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="af694-432">Don't make these code changes if you completed the previous section and updated the database.</span></span>

<span data-ttu-id="af694-433">*{Timestamp}_ComplexDataModel.cs*檔案包含下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="af694-433">The *{timestamp}_ComplexDataModel.cs* file contains the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_DepartmentID)]

<span data-ttu-id="af694-434">上述程式碼中加入不可為 null`DepartmentID`至 FK`Course`資料表。</span><span class="sxs-lookup"><span data-stu-id="af694-434">The preceding code adds a non-nullable `DepartmentID` FK to the `Course` table.</span></span> <span data-ttu-id="af694-435">包含資料列中的，從上一個教學課程 DB `Course`，因此無法更新移轉該資料表。</span><span class="sxs-lookup"><span data-stu-id="af694-435">The DB from the previous tutorial contains rows in `Course`, so that table cannot be updated by migrations.</span></span>

<span data-ttu-id="af694-436">若要讓`ComplexDataModel`的現有資料的移轉工作：</span><span class="sxs-lookup"><span data-stu-id="af694-436">To make the `ComplexDataModel` migration work with existing data:</span></span>

* <span data-ttu-id="af694-437">變更程式碼，讓新的資料行 (`DepartmentID`) 預設值。</span><span class="sxs-lookup"><span data-stu-id="af694-437">Change the code to give the new column (`DepartmentID`) a default value.</span></span>
* <span data-ttu-id="af694-438">建立名為"Temp"做為預設部門假部門。</span><span class="sxs-lookup"><span data-stu-id="af694-438">Create a fake department named "Temp" to act as the default department.</span></span>

### <a name="fix-the-foreign-key-constraints"></a><span data-ttu-id="af694-439">修正 foreign key 條件約束</span><span class="sxs-lookup"><span data-stu-id="af694-439">Fix the foreign key constraints</span></span>

<span data-ttu-id="af694-440">更新`ComplexDataModel`類別`Up`方法：</span><span class="sxs-lookup"><span data-stu-id="af694-440">Update the `ComplexDataModel` classes `Up` method:</span></span>

* <span data-ttu-id="af694-441">開啟*{timestamp}_ComplexDataModel.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="af694-441">Open the *{timestamp}_ComplexDataModel.cs* file.</span></span>
* <span data-ttu-id="af694-442">註解新增的程式碼行`DepartmentID`欄`Course`資料表。</span><span class="sxs-lookup"><span data-stu-id="af694-442">Comment out the line of code that adds the `DepartmentID` column to the `Course` table.</span></span>

[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CommentOut&highlight=9-13)]

<span data-ttu-id="af694-443">加入下列反白顯示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="af694-443">Add the following highlighted code.</span></span> <span data-ttu-id="af694-444">新的程式碼會進入之後`.CreateTable( name: "Department"`區塊：[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CreateDefaultValue&highlight=22-32)]</span><span class="sxs-lookup"><span data-stu-id="af694-444">The new code goes after the `.CreateTable( name: "Department"` block: [!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CreateDefaultValue&highlight=22-32)]</span></span>

<span data-ttu-id="af694-445">上述變更，現存`Course`將相關資料列之後的"Temp"部門`ComplexDataModel``Up`方法執行。</span><span class="sxs-lookup"><span data-stu-id="af694-445">With the preceding changes, existing `Course` rows will be related to the "Temp" department after the `ComplexDataModel` `Up` method runs.</span></span>

<span data-ttu-id="af694-446">在生產應用程式會：</span><span class="sxs-lookup"><span data-stu-id="af694-446">A production app would:</span></span>

* <span data-ttu-id="af694-447">包含程式碼或指令碼，以新增`Department`的資料列和相關`Course`至新的資料列`Department`資料列。</span><span class="sxs-lookup"><span data-stu-id="af694-447">Include code or scripts to add `Department` rows and related `Course` rows to the new `Department` rows.</span></span>
* <span data-ttu-id="af694-448">不會使用"Temp"部門的預設值為`Course.DepartmentID `。</span><span class="sxs-lookup"><span data-stu-id="af694-448">Would not use the "Temp" department or the default value for `Course.DepartmentID `.</span></span>

<span data-ttu-id="af694-449">下一個教學課程涵蓋相關的資料。</span><span class="sxs-lookup"><span data-stu-id="af694-449">The next tutorial covers related data.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="af694-450">[上一頁](xref:data/ef-rp/migrations)
[下一頁](xref:data/ef-rp/read-related-data)</span><span class="sxs-lookup"><span data-stu-id="af694-450">[Previous](xref:data/ef-rp/migrations)
[Next](xref:data/ef-rp/read-related-data)</span></span>