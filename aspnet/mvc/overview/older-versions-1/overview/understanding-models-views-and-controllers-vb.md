---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-vb
title: "了解模型、 檢視和控制站 (VB) |Microsoft 文件"
author: StephenWalther
description: "搞不清楚模型、 檢視和控制器嗎？ 在本教學課程中，作者： Stephen Walther 向您介紹 ASP.NET MVC 應用程式的不同部分。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: a106374a-5e74-4fd0-9ac0-1a32280e5d0d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-vb
msc.type: authoredcontent
ms.openlocfilehash: 36f70503f7e96210e5fb8a2d361da6759c18c85b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/10/2017
---
<a name="understanding-models-views-and-controllers-vb"></a><span data-ttu-id="8cc0c-104">了解模型、 檢視和控制站 (VB)</span><span class="sxs-lookup"><span data-stu-id="8cc0c-104">Understanding Models, Views, and Controllers (VB)</span></span>
====================
<span data-ttu-id="8cc0c-105">由[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="8cc0c-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="8cc0c-106">搞不清楚模型、 檢視和控制器嗎？</span><span class="sxs-lookup"><span data-stu-id="8cc0c-106">Confused about Models, Views, and Controllers?</span></span> <span data-ttu-id="8cc0c-107">在本教學課程中，作者： Stephen Walther 向您介紹 ASP.NET MVC 應用程式的不同部分。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-107">In this tutorial, Stephen Walther introduces you to the different parts of an ASP.NET MVC application.</span></span>


<span data-ttu-id="8cc0c-108">本教學課程為您提供的高階概觀 ASP.NET MVC 模型、 檢視和控制器。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-108">This tutorial provides you with a high-level overview of ASP.NET MVC models, views, and controllers.</span></span> <span data-ttu-id="8cc0c-109">換句話說，它會說明 M'，V'，與 C' ASP.NET MVC 中。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-109">In other words, it explains the M', V', and C' in ASP.NET MVC.</span></span>

<span data-ttu-id="8cc0c-110">閱讀本教學課程之後, 您應該了解 ASP.NET MVC 應用程式的不同部分如何一起運作。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-110">After reading this tutorial, you should understand how the different parts of an ASP.NET MVC application work together.</span></span> <span data-ttu-id="8cc0c-111">您也應該了解 ASP.NET MVC 應用程式的架構不同於 ASP.NET Web Form 應用程式或動態伺服器網頁應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-111">You should also understand how the architecture of an ASP.NET MVC application differs from an ASP.NET Web Forms application or Active Server Pages application.</span></span>

## <a name="the-sample-aspnet-mvc-application"></a><span data-ttu-id="8cc0c-112">範例 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="8cc0c-112">The Sample ASP.NET MVC Application</span></span>

<span data-ttu-id="8cc0c-113">建立 ASP.NET MVC Web 應用程式的預設 Visual Studio 範本包含非常簡單的範例應用程式，可用來了解 ASP.NET MVC 應用程式的不同部分。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-113">The default Visual Studio template for creating ASP.NET MVC Web Applications includes an extremely simple sample application that can be used to understand the different parts of an ASP.NET MVC application.</span></span> <span data-ttu-id="8cc0c-114">我們會利用這個簡單的應用程式，在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-114">We take advantage of this simple application in this tutorial.</span></span>

<span data-ttu-id="8cc0c-115">與 MVC 範本建立新的 ASP.NET MVC 應用程式啟動 Visual Studio 2008 中，選取 [檔案] 功能表選項，新增專案 （請參閱圖 1）。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-115">You create a new ASP.NET MVC application with the MVC template by launching Visual Studio 2008 and selecting the menu option File, New Project (see Figure 1).</span></span> <span data-ttu-id="8cc0c-116">在 新增專案 對話方塊中，選取 專案類型 (Visual Basic 或 C#） 您最愛的程式語言，然後選取**ASP.NET MVC Web 應用程式**範本下。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-116">In the New Project dialog, select your favorite programming language under Project Types (Visual Basic or C#) and select **ASP.NET MVC Web Application** under Templates.</span></span> <span data-ttu-id="8cc0c-117">按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-117">Click the OK button.</span></span>


<span data-ttu-id="8cc0c-118">[![新增專案 對話方塊](understanding-models-views-and-controllers-vb/_static/image1.jpg)](understanding-models-views-and-controllers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8cc0c-118">[![New Project Dialog](understanding-models-views-and-controllers-vb/_static/image1.jpg)](understanding-models-views-and-controllers-vb/_static/image1.png)</span></span>

<span data-ttu-id="8cc0c-119">**圖 01**： 新增專案 對話方塊 ([按一下以檢視完整大小的影像](understanding-models-views-and-controllers-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="8cc0c-119">**Figure 01**: New Project Dialog ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image2.png))</span></span>


<span data-ttu-id="8cc0c-120">當您建立新的 ASP.NET MVC 應用程式，**建立單元測試專案**對話方塊隨即出現 （請參閱圖 2）。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-120">When you create a new ASP.NET MVC application, the **Create Unit Test Project** dialog appears (see Figure 2).</span></span> <span data-ttu-id="8cc0c-121">這個對話方塊可讓您以測試 ASP.NET MVC 應用程式在方案中建立個別的專案。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-121">This dialog enables you to create a separate project in your solution for testing your ASP.NET MVC application.</span></span> <span data-ttu-id="8cc0c-122">選取的選項**否，不要建立單元測試專案**按一下**確定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-122">Select the option **No, do not create a unit test project** and click the **OK** button.</span></span>


<span data-ttu-id="8cc0c-123">[![建立單元測試 對話方塊](understanding-models-views-and-controllers-vb/_static/image2.jpg)](understanding-models-views-and-controllers-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="8cc0c-123">[![Create Unit Test Dialog](understanding-models-views-and-controllers-vb/_static/image2.jpg)](understanding-models-views-and-controllers-vb/_static/image3.png)</span></span>

<span data-ttu-id="8cc0c-124">**圖 02**： 建立單元測試對話方塊 ([按一下以檢視完整大小的影像](understanding-models-views-and-controllers-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="8cc0c-124">**Figure 02**: Create Unit Test Dialog ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image4.png))</span></span>


<span data-ttu-id="8cc0c-125">新的 ASP.NET MVC 應用程式建立之後。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-125">After the new ASP.NET MVC application is created.</span></span> <span data-ttu-id="8cc0c-126">您會看到數個資料夾和 [方案總管] 視窗中的檔案。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-126">You will see several folders and files in the Solution Explorer window.</span></span> <span data-ttu-id="8cc0c-127">特別是，您會看到名為模型、 檢視和控制器的三個資料夾。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-127">In particular, you'll see three folders named Models, Views, and Controllers.</span></span> <span data-ttu-id="8cc0c-128">您猜的資料夾名稱，這些資料夾包含實作模型、 檢視和控制器的檔案。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-128">As you might guess from the folder names, these folders contain the files for implementing models, views, and controllers.</span></span>

<span data-ttu-id="8cc0c-129">如果您展開 Controllers 資料夾，您應該會看到名為 AccountController.vb 和名為 HomeController.vb 的檔案。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-129">If you expand the Controllers folder, you should see a file named AccountController.vb and a file named HomeController.vb.</span></span> <span data-ttu-id="8cc0c-130">如果您展開 [檢視] 資料夾，您應該會看到三個名為帳戶首頁] 和 [共用的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-130">If you expand the Views folder, you should see three subfolders named Account, Home and Shared.</span></span> <span data-ttu-id="8cc0c-131">如果您展開 Home 資料夾，您會看到兩個名為 about.aspx 的網頁和 Index.aspx （請參閱圖 3） 的其他檔案。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-131">If you expand the Home folder, you'll see two additional files named About.aspx and Index.aspx (see Figure 3).</span></span> <span data-ttu-id="8cc0c-132">這些檔案便會產生預設的 ASP.NET MVC 範本所隨附的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-132">These files make up the sample application included with the default ASP.NET MVC template.</span></span>


<span data-ttu-id="8cc0c-133">[![[方案總管] 視窗](understanding-models-views-and-controllers-vb/_static/image3.jpg)](understanding-models-views-and-controllers-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="8cc0c-133">[![The Solution Explorer Window](understanding-models-views-and-controllers-vb/_static/image3.jpg)](understanding-models-views-and-controllers-vb/_static/image5.png)</span></span>

<span data-ttu-id="8cc0c-134">**圖 03**: 方案總管 視窗 ([按一下以檢視完整大小的影像](understanding-models-views-and-controllers-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="8cc0c-134">**Figure 03**: The Solution Explorer Window ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image6.png))</span></span>


<span data-ttu-id="8cc0c-135">您可以藉由選取功能表選項來執行範例應用程式**偵錯，開始偵錯**。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-135">You can run the sample application by selecting the menu option **Debug, Start Debugging**.</span></span> <span data-ttu-id="8cc0c-136">或者，您可以按 F5 鍵。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-136">Alternatively, you can press the F5 key.</span></span>

<span data-ttu-id="8cc0c-137">當您第一次執行 ASP.NET 應用程式時，在圖 4 對話方塊隨即出現，建議您啟用偵錯模式。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-137">When you first run an ASP.NET application, the dialog in Figure 4 appears that recommends that you enable debug mode.</span></span> <span data-ttu-id="8cc0c-138">按一下 [確定] 按鈕，而且應用程式會執行。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-138">Click the OK button and the application will run.</span></span>


<span data-ttu-id="8cc0c-139">[![未啟用的偵錯對話方塊](understanding-models-views-and-controllers-vb/_static/image4.jpg)](understanding-models-views-and-controllers-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="8cc0c-139">[![Debugging Not Enabled dialog](understanding-models-views-and-controllers-vb/_static/image4.jpg)](understanding-models-views-and-controllers-vb/_static/image7.png)</span></span>

<span data-ttu-id="8cc0c-140">**圖 04**： 未啟用偵錯對話方塊 ([按一下以檢視完整大小的影像](understanding-models-views-and-controllers-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="8cc0c-140">**Figure 04**: Debugging Not Enabled dialog ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image8.png))</span></span>


<span data-ttu-id="8cc0c-141">當您執行 ASP.NET MVC 應用程式時，Visual Studio 會啟動網頁瀏覽器中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-141">When you run an ASP.NET MVC application, Visual Studio launches the application in your web browser.</span></span> <span data-ttu-id="8cc0c-142">範例應用程式只有兩個頁面所組成： 索引頁面和 [關於] 頁面。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-142">The sample application consists of only two pages: the Index page and the About page.</span></span> <span data-ttu-id="8cc0c-143">當應用程式第一次啟動時，索引頁會出現 （請參閱圖 5）。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-143">When the application first starts, the Index page appears (see Figure 5).</span></span> <span data-ttu-id="8cc0c-144">您可以導覽至 [關於] 頁面按一下頂端的功能表連結應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-144">You can navigate to the About page by clicking the menu link at the top right of the application.</span></span>


<span data-ttu-id="8cc0c-145">[![索引頁](understanding-models-views-and-controllers-vb/_static/image5.jpg)](understanding-models-views-and-controllers-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="8cc0c-145">[![The Index Page](understanding-models-views-and-controllers-vb/_static/image5.jpg)](understanding-models-views-and-controllers-vb/_static/image9.png)</span></span>

<span data-ttu-id="8cc0c-146">**圖 05**: 索引頁 ([按一下以檢視完整大小的影像](understanding-models-views-and-controllers-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="8cc0c-146">**Figure 05**: The Index Page ([Click to view full-size image](understanding-models-views-and-controllers-vb/_static/image10.png))</span></span>


<span data-ttu-id="8cc0c-147">請注意您的瀏覽器的網址列中的 Url。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-147">Notice the URLs in the address bar of your browser.</span></span> <span data-ttu-id="8cc0c-148">例如，當您按一下 [關於] 功能表的連結，在瀏覽器網址列中的 URL 變更為**/家用] / [關於**。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-148">For example, when you click the About menu link, the URL in the browser address bar changes to **/Home/About**.</span></span>

<span data-ttu-id="8cc0c-149">如果您關閉瀏覽器視窗並返回 Visual Studio，將無法與路徑首頁/約尋找檔案。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-149">If you close the browser window and return to Visual Studio, you won't be able to find a file with the path Home/About.</span></span> <span data-ttu-id="8cc0c-150">檔案不存在。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-150">The files don't exist.</span></span> <span data-ttu-id="8cc0c-151">如何這可能會？</span><span class="sxs-lookup"><span data-stu-id="8cc0c-151">How is this possible?</span></span>

## <a name="a-url-does-not-equal-a-page"></a><span data-ttu-id="8cc0c-152">URL 不等於頁面</span><span class="sxs-lookup"><span data-stu-id="8cc0c-152">A URL Does Not Equal a Page</span></span>

<span data-ttu-id="8cc0c-153">當您建置傳統的 ASP.NET Web Form 應用程式或動態伺服器網頁應用程式時，但沒有 URL 和頁面之間的一對一對應。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-153">When you build a traditional ASP.NET Web Forms application or an Active Server Pages application, there is a one-to-one correspondence between a URL and a page.</span></span> <span data-ttu-id="8cc0c-154">如果您要求從伺服器名為 SomePage.aspx 的頁面，然後有更有頁面 SomePage.aspx 名為的磁碟上。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-154">If you request a page named SomePage.aspx from the server, then there had better be a page on disk named SomePage.aspx.</span></span> <span data-ttu-id="8cc0c-155">如果 SomePage.aspx 檔案不存在，您會收到優劣**404-找不到頁面**錯誤。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-155">If the SomePage.aspx file does not exist, you get an ugly **404 - Page Not Found** error.</span></span>

<span data-ttu-id="8cc0c-156">建置 ASP.NET MVC 應用程式時，相較之下，沒有任何您在瀏覽器的網址列輸入的 URL 與您在您的應用程式中找到的檔案之間的對應。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-156">When building an ASP.NET MVC application, in contrast, there is no correspondence between the URL that you type into your browser's address bar and the files that you find in your application.</span></span> <span data-ttu-id="8cc0c-157">在 ASP.NET MVC 應用程式 URL 對應至控制器動作，而不是磁碟上的頁面。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-157">In an ASP.NET MVC application, a URL corresponds to a controller action instead of a page on disk.</span></span>

<span data-ttu-id="8cc0c-158">在傳統 ASP.NET 或 ASP 應用程式中，瀏覽器要求，會對應至頁面。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-158">In a traditional ASP.NET or ASP application, browser requests are mapped to pages.</span></span> <span data-ttu-id="8cc0c-159">相反地，ASP.NET MVC 應用程式中，瀏覽器要求，會對應至控制器的動作。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-159">In an ASP.NET MVC application, in contrast, browser requests are mapped to controller actions.</span></span> <span data-ttu-id="8cc0c-160">ASP.NET Web Form 應用程式是以內容為中心。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-160">An ASP.NET Web Forms application is content-centric.</span></span> <span data-ttu-id="8cc0c-161">ASP.NET MVC 應用程式相較之下，為中心的應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-161">An ASP.NET MVC application, in contrast, is application logic centric.</span></span>

## <a name="understanding-aspnet-routing"></a><span data-ttu-id="8cc0c-162">了解 ASP.NET 路由</span><span class="sxs-lookup"><span data-stu-id="8cc0c-162">Understanding ASP.NET Routing</span></span>

<span data-ttu-id="8cc0c-163">瀏覽器要求對應至呼叫的 ASP.NET framework 功能透過控制器動作*ASP.NET 路由*。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-163">A browser request gets mapped to a controller action through a feature of the ASP.NET framework called *ASP.NET Routing*.</span></span> <span data-ttu-id="8cc0c-164">ASP.NET 路由正由 ASP.NET MVC 架構*路由*控制器動作的內送要求。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-164">ASP.NET Routing is used by the ASP.NET MVC framework to *route* incoming requests to controller actions.</span></span>

<span data-ttu-id="8cc0c-165">ASP.NET 路由會使用路由表，來處理傳入要求。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-165">ASP.NET Routing uses a route table to handle incoming requests.</span></span> <span data-ttu-id="8cc0c-166">Web 應用程式第一次啟動時，會建立此路由表。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-166">This route table is created when your web application first starts.</span></span> <span data-ttu-id="8cc0c-167">路由表是在 Global.asax 檔案中的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-167">The route table is setup in the Global.asax file.</span></span> <span data-ttu-id="8cc0c-168">預設的 MVC Global.asax 檔案包含在程式碼範例 1。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-168">The default MVC Global.asax file is contained in Listing 1.</span></span>

<span data-ttu-id="8cc0c-169">**列出 1-Global.asax**</span><span class="sxs-lookup"><span data-stu-id="8cc0c-169">**Listing 1 - Global.asax**</span></span>

[!code-vb[Main](understanding-models-views-and-controllers-vb/samples/sample1.vb)]

<span data-ttu-id="8cc0c-170">ASP.NET 應用程式第一次啟動時，應用程式\_呼叫 start （） 方法。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-170">When an ASP.NET application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="8cc0c-171">在清單 1 中，這個方法會呼叫 RegisterRoutes() 方法和 RegisterRoutes() 方法會建立預設路由表。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-171">In Listing 1, this method calls the RegisterRoutes() method and the RegisterRoutes() method creates the default route table.</span></span>

<span data-ttu-id="8cc0c-172">預設路由表包含一個路由。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-172">The default route table consists of one route.</span></span> <span data-ttu-id="8cc0c-173">這個預設路由中分成三個區段 （URL 區段是正斜線之間的任何項目） 的所有連入要求。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-173">This default route breaks all incoming requests into three segments (a URL segment is anything between forward slashes).</span></span> <span data-ttu-id="8cc0c-174">第一個區段對應至控制器名稱、 第二個區段都會對應到動作名稱，以及最後區段對應到參數傳遞給名為識別碼的動作</span><span class="sxs-lookup"><span data-stu-id="8cc0c-174">The first segment is mapped to a controller name, the second segment is mapped to an action name, and the final segment is mapped to a parameter passed to the action named Id.</span></span>

<span data-ttu-id="8cc0c-175">例如，請考慮下列 URL:</span><span class="sxs-lookup"><span data-stu-id="8cc0c-175">For example, consider the following URL:</span></span>

<span data-ttu-id="8cc0c-176">/ 產品/詳細資料/3</span><span class="sxs-lookup"><span data-stu-id="8cc0c-176">/Product/Details/3</span></span>

<span data-ttu-id="8cc0c-177">此 URL 會剖析成三個參數，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="8cc0c-177">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="8cc0c-178">控制器 = 產品</span><span class="sxs-lookup"><span data-stu-id="8cc0c-178">Controller = Product</span></span>

<span data-ttu-id="8cc0c-179">動作 = 詳細資料</span><span class="sxs-lookup"><span data-stu-id="8cc0c-179">Action = Details</span></span>

<span data-ttu-id="8cc0c-180">識別碼 = 3</span><span class="sxs-lookup"><span data-stu-id="8cc0c-180">Id = 3</span></span>

<span data-ttu-id="8cc0c-181">在 Global.asax 檔中定義的預設路由包含所有的三個參數的預設值。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-181">The Default route defined in the Global.asax file includes default values for all three parameters.</span></span> <span data-ttu-id="8cc0c-182">預設控制器為首頁、 預設動作是索引，而識別碼的預設值為空字串。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-182">The default Controller is Home, the default Action is Index, and the default Id is an empty string.</span></span> <span data-ttu-id="8cc0c-183">請注意這些預設值，請考慮下列 URL 剖析的方式：</span><span class="sxs-lookup"><span data-stu-id="8cc0c-183">With these defaults in mind, consider how the following URL is parsed:</span></span>

<span data-ttu-id="8cc0c-184">/ 所有員工</span><span class="sxs-lookup"><span data-stu-id="8cc0c-184">/Employee</span></span>

<span data-ttu-id="8cc0c-185">此 URL 會剖析成三個參數，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="8cc0c-185">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="8cc0c-186">控制器 = 員工</span><span class="sxs-lookup"><span data-stu-id="8cc0c-186">Controller = Employee</span></span>

<span data-ttu-id="8cc0c-187">動作 = 索引</span><span class="sxs-lookup"><span data-stu-id="8cc0c-187">Action = Index</span></span>

<span data-ttu-id="8cc0c-188">識別碼 =</span><span class="sxs-lookup"><span data-stu-id="8cc0c-188">Id = ��</span></span>

<span data-ttu-id="8cc0c-189">最後，如果您未提供任何 URL 開啟 ASP.NET MVC 應用程式 (例如， `http://localhost`) 將 URL 會剖析像這樣：</span><span class="sxs-lookup"><span data-stu-id="8cc0c-189">Finally, if you open an ASP.NET MVC Application without supplying any URL (for example, `http://localhost`) then the URL is parsed like this:</span></span>

<span data-ttu-id="8cc0c-190">控制器 = Home</span><span class="sxs-lookup"><span data-stu-id="8cc0c-190">Controller = Home</span></span>

<span data-ttu-id="8cc0c-191">動作 = 索引</span><span class="sxs-lookup"><span data-stu-id="8cc0c-191">Action = Index</span></span>

<span data-ttu-id="8cc0c-192">識別碼 =</span><span class="sxs-lookup"><span data-stu-id="8cc0c-192">Id = ��</span></span>

<span data-ttu-id="8cc0c-193">要求會路由至 HomeController 類別中的 index 動作。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-193">The request is routed to the Index() action on the HomeController class.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="8cc0c-194">了解控制器</span><span class="sxs-lookup"><span data-stu-id="8cc0c-194">Understanding Controllers</span></span>

<span data-ttu-id="8cc0c-195">控制器負責控制使用者與 MVC 應用程式互動的方式。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-195">A controller is responsible for controlling the way that a user interacts with an MVC application.</span></span> <span data-ttu-id="8cc0c-196">控制器包含 ASP.NET MVC 應用程式的流程控制邏輯。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-196">A controller contains the flow control logic for an ASP.NET MVC application.</span></span> <span data-ttu-id="8cc0c-197">控制器會決定哪些回應傳送回給使用者，當使用者瀏覽器要求。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-197">A controller determines what response to send back to a user when a user makes a browser request.</span></span>

<span data-ttu-id="8cc0c-198">在控制站是只類別 （例如，Visual Basic 或 C# 類別）。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-198">A controller is just a class (for example, a Visual Basic or C# class).</span></span> <span data-ttu-id="8cc0c-199">此範例的 ASP.NET MVC 應用程式包含名為 HomeController.vb 位於 [控制器] 資料夾中的控制站。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-199">The sample ASP.NET MVC application includes a controller named HomeController.vb located in the Controllers folder.</span></span> <span data-ttu-id="8cc0c-200">列出 2 中重現 HomeController.vb 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-200">The content of the HomeController.vb file is reproduced in Listing 2.</span></span>

<span data-ttu-id="8cc0c-201">**列出 2-HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="8cc0c-201">**Listing 2 - HomeController.cs**</span></span>

[!code-vb[Main](understanding-models-views-and-controllers-vb/samples/sample2.vb)]

<span data-ttu-id="8cc0c-202">請注意 HomeController 有兩個名為 index （） 和 about 的方法。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-202">Notice that the HomeController has two methods named Index() and About().</span></span> <span data-ttu-id="8cc0c-203">這兩種方法對應到兩個控制器所公開的動作。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-203">These two methods correspond to the two actions exposed by the controller.</span></span> <span data-ttu-id="8cc0c-204">URL /Home/索引叫用 HomeController.Index() 方法和 URL /Home/需叫用 HomeController.About() 方法。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-204">The URL /Home/Index invokes the HomeController.Index() method and the URL /Home/About invokes the HomeController.About() method.</span></span>

<span data-ttu-id="8cc0c-205">在控制器中的任何公用方法會公開為控制器動作。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-205">Any public method in a controller is exposed as a controller action.</span></span> <span data-ttu-id="8cc0c-206">您需要謹慎這。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-206">You need to be careful about this.</span></span> <span data-ttu-id="8cc0c-207">這表示，在控制器中包含任何公用方法可以叫用具有網際網路存取權的任何人都將正確的 URL 輸入瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-207">This means that any public method contained in a controller can be invoked by anyone with access to the Internet by entering the right URL into a browser.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="8cc0c-208">了解檢視</span><span class="sxs-lookup"><span data-stu-id="8cc0c-208">Understanding Views</span></span>

<span data-ttu-id="8cc0c-209">兩個控制器的動作由 HomeController 類別，index （） 和 about，兩者都傳回檢視表。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-209">The two controller actions exposed by the HomeController class, Index() and About(), both return a view.</span></span> <span data-ttu-id="8cc0c-210">檢視包含的 HTML 標記和傳送到瀏覽器的內容。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-210">A view contains the HTML markup and content that is sent to the browser.</span></span> <span data-ttu-id="8cc0c-211">使用 ASP.NET MVC 應用程式時，檢視是網頁的對等項目。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-211">A view is the equivalent of a page when working with an ASP.NET MVC application.</span></span>

<span data-ttu-id="8cc0c-212">您必須建立您的檢視，在正確的位置。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-212">You must create your views in the right location.</span></span> <span data-ttu-id="8cc0c-213">HomeController.Index() 動作將會傳回檢視位於下列路徑：</span><span class="sxs-lookup"><span data-stu-id="8cc0c-213">The HomeController.Index() action returns a view located at the following path:</span></span>

<span data-ttu-id="8cc0c-214">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="8cc0c-214">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="8cc0c-215">HomeController.About() 動作將會傳回檢視位於下列路徑：</span><span class="sxs-lookup"><span data-stu-id="8cc0c-215">The HomeController.About() action returns a view located at the following path:</span></span>

<span data-ttu-id="8cc0c-216">\Views\Home\About.aspx</span><span class="sxs-lookup"><span data-stu-id="8cc0c-216">\Views\Home\About.aspx</span></span>

<span data-ttu-id="8cc0c-217">一般情況下，如果您想要傳回控制器動作的檢視，然後您要在與您的控制器名稱相同的 [檢視] 資料夾中建立子資料夾。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-217">In general, if you want to return a view for a controller action, then you need to create a subfolder in the Views folder with the same name as your controller.</span></span> <span data-ttu-id="8cc0c-218">中子資料夾中，您必須建立.aspx 檔案具有相同名稱做為控制器動作。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-218">Within the subfolder, you must create an .aspx file with the same name as the controller action.</span></span>

<span data-ttu-id="8cc0c-219">列出的 3 中的檔案包含 about.aspx 的網頁檢視。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-219">The file in Listing 3 contains the About.aspx view.</span></span>

<span data-ttu-id="8cc0c-220">**列出 3-about.aspx 的網頁**</span><span class="sxs-lookup"><span data-stu-id="8cc0c-220">**Listing 3 - About.aspx**</span></span>

[!code-aspx[Main](understanding-models-views-and-controllers-vb/samples/sample3.aspx)]

<span data-ttu-id="8cc0c-221">如果您忽略列表 3 中的第一行，大部分的檢視的其餘部分所組成標準 HTML。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-221">If you ignore the first line in Listing 3, most of the rest of the view consists of standard HTML.</span></span> <span data-ttu-id="8cc0c-222">您可以輸入任何您想要的 HTML 修改檢視的內容。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-222">You can modify the contents of the view by entering any HTML that you want here.</span></span>

<span data-ttu-id="8cc0c-223">檢視是非常類似於 Active Server Pages 或 ASP.NET Web Form 中的頁面。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-223">A view is very similar to a page in Active Server Pages or ASP.NET Web Forms.</span></span> <span data-ttu-id="8cc0c-224">檢視可以包含 HTML 內容和指令碼。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-224">A view can contain HTML content and scripts.</span></span> <span data-ttu-id="8cc0c-225">您可以撰寫指令碼，在您最愛的.NET 程式語言 （例如，C# 或 Visual Basic.NET）。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-225">You can write the scripts in your favorite .NET programming language (for example, C# or Visual Basic .NET).</span></span> <span data-ttu-id="8cc0c-226">您可以使用指令碼來顯示動態內容，例如資料庫的資料。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-226">You use scripts to display dynamic content such as database data.</span></span>

## <a name="understanding-models"></a><span data-ttu-id="8cc0c-227">了解模型</span><span class="sxs-lookup"><span data-stu-id="8cc0c-227">Understanding Models</span></span>

<span data-ttu-id="8cc0c-228">我們已經討論過控制站，我們已經討論過的檢視。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-228">We have discussed controllers and we have discussed views.</span></span> <span data-ttu-id="8cc0c-229">最後一個我們要討論的主題是模型。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-229">The last topic that we need to discuss is models.</span></span> <span data-ttu-id="8cc0c-230">MVC 模型是什麼？</span><span class="sxs-lookup"><span data-stu-id="8cc0c-230">What is an MVC model?</span></span>

<span data-ttu-id="8cc0c-231">MVC 模型包含的所有應用程式邏輯，並未包含在檢視或控制站。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-231">An MVC model contains all of your application logic that is not contained in a view or a controller.</span></span> <span data-ttu-id="8cc0c-232">模型應包含所有的應用程式商務邏輯，驗證邏輯和資料庫存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-232">The model should contain all of your application business logic, validation logic, and database access logic.</span></span> <span data-ttu-id="8cc0c-233">比方說，如果您使用 Microsoft Entity Framework 來存取您的資料庫，然後您會建立您 Entity Framework 類別 （在.edmx 檔案） 在 [模型] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-233">For example, if you are using the Microsoft Entity Framework to access your database, then you would create your Entity Framework classes (your .edmx file) in the Models folder.</span></span>

<span data-ttu-id="8cc0c-234">檢視應該包含相關以產生使用者介面的邏輯。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-234">A view should contain only logic related to generating the user interface.</span></span> <span data-ttu-id="8cc0c-235">在控制站應該只包含邏輯傳回右方檢視，或將使用者重新導向至另一個動作 （流量控制） 所需的最低限度。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-235">A controller should only contain the bare minimum of logic required to return the right view or redirect the user to another action (flow control).</span></span> <span data-ttu-id="8cc0c-236">所有其他項目應包含在模型中。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-236">Everything else should be contained in the model.</span></span>

<span data-ttu-id="8cc0c-237">一般情況下，您應盡可能 fat 模型和 skinny 控制站。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-237">In general, you should strive for fat models and skinny controllers.</span></span> <span data-ttu-id="8cc0c-238">控制器方法應只有幾行程式碼。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-238">Your controller methods should contain only a few lines of code.</span></span> <span data-ttu-id="8cc0c-239">如果太 fat 控制器動作，您應該考慮將邏輯移到 [模型] 資料夾中的新類別。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-239">If a controller action gets too fat, then you should consider moving the logic out to a new class in the Models folder.</span></span>

## <a name="summary"></a><span data-ttu-id="8cc0c-240">總結</span><span class="sxs-lookup"><span data-stu-id="8cc0c-240">Summary</span></span>

<span data-ttu-id="8cc0c-241">本教學課程提供您的 ASP.NET MVC 的不同部分的高層級概觀 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-241">This tutorial provided you with a high level overview of the different parts of an ASP.NET MVC web application.</span></span> <span data-ttu-id="8cc0c-242">您已學習如何 ASP.NET 路由傳入瀏覽器將要求對應至特定控制器的動作。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-242">You learned how ASP.NET Routing maps incoming browser requests to particular controller actions.</span></span> <span data-ttu-id="8cc0c-243">您已學習如何控制站協調瀏覽器傳回檢視的方式。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-243">You learned how controllers orchestrate how views are returned to the browser.</span></span> <span data-ttu-id="8cc0c-244">最後，您學到如何模型包含應用程式商務、 驗證和資料庫存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="8cc0c-244">Finally, you learned how models contain application business, validation, and database access logic.</span></span>