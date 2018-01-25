---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
title: "建立和封裝 Web 應用程式專案 |Microsoft 文件"
author: jrjlee
description: "當您想要將 web 應用程式專案部署到遠端伺服器環境時，您的第一個工作是建置專案，並產生 web 部署 packa..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 94e92f80-a7e3-4d18-9375-ff8be5d666ac
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
msc.type: authoredcontent
ms.openlocfilehash: c05f725c9e6b493a6af8f5b5d20dbc9ff73a1ef8
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/10/2017
---
<a name="building-and-packaging-web-application-projects"></a><span data-ttu-id="5385c-103">建立和封裝 Web 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="5385c-103">Building and Packaging Web Application Projects</span></span>
====================
<span data-ttu-id="5385c-104">由[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="5385c-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="5385c-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="5385c-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="5385c-106">當您想要將 web 應用程式專案部署到遠端伺服器環境時，您的第一個工作是建置專案，並產生 web 部署套件。</span><span class="sxs-lookup"><span data-stu-id="5385c-106">When you want to deploy a web application project to a remote server environment, your first task is to build the project and generate a web deployment package.</span></span> <span data-ttu-id="5385c-107">本主題說明如何建置程序適用於 web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="5385c-107">This topic describes how the build process works for web application projects.</span></span> <span data-ttu-id="5385c-108">特別是，它會說明：</span><span class="sxs-lookup"><span data-stu-id="5385c-108">In particular, it explains:</span></span>
> 
> - <span data-ttu-id="5385c-109">如何 Web 發行管線 (WPP) 擴充建置程序，以包含部署的功能。</span><span class="sxs-lookup"><span data-stu-id="5385c-109">How the Web Publishing Pipeline (WPP) extends the build process to include deployment functionality.</span></span>
> - <span data-ttu-id="5385c-110">如何網際網路資訊服務 (IIS) Web Deployment Tool (Web Deploy) 會開啟您的 web 應用程式，到部署套件。</span><span class="sxs-lookup"><span data-stu-id="5385c-110">How the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) turns your web application into a deployment package.</span></span>
> - <span data-ttu-id="5385c-111">如何建置和封裝程序運作，並建立哪些檔案。</span><span class="sxs-lookup"><span data-stu-id="5385c-111">How the build and packaging process works and what files are created.</span></span>


<span data-ttu-id="5385c-112">在 Visual Studio 2010、 WPP 支援 web 應用程式專案的建置和部署程序。</span><span class="sxs-lookup"><span data-stu-id="5385c-112">In Visual Studio 2010, the build and deployment process for web application projects is supported by the WPP.</span></span> <span data-ttu-id="5385c-113">WPP 提供擴充功能的 MSBuild 並啟用整合與 Web Deploy 的 Microsoft Build Engine (MSBuild) 目標的集。</span><span class="sxs-lookup"><span data-stu-id="5385c-113">The WPP provides a set of Microsoft Build Engine (MSBuild) targets that extend the functionality of MSBuild and enable it to integrate with Web Deploy.</span></span> <span data-ttu-id="5385c-114">在 Visual Studio 中，您可以看到這項擴充的功能屬性頁上 web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="5385c-114">Within Visual Studio, you can see this extended functionality on the property pages for your web application project.</span></span> <span data-ttu-id="5385c-115">**封裝/發行 Web**頁面上，搭配**封裝/發行 SQL**頁面上，可讓您設定建置程序完成後您的 web 應用程式專案會封裝部署的方式。</span><span class="sxs-lookup"><span data-stu-id="5385c-115">The **Package/Publish Web** page, together with the **Package/Publish SQL** page, lets you configure how your web application project is packaged for deployment when the build process is complete.</span></span>

![](building-and-packaging-web-application-projects/_static/image1.png)

## <a name="how-does-the-wpp-work"></a><span data-ttu-id="5385c-116">WPP 的運作方式為何？</span><span class="sxs-lookup"><span data-stu-id="5385c-116">How Does the WPP Work?</span></span>

<span data-ttu-id="5385c-117">如果您看一下專案檔的 C# 為基礎的 web 應用程式專案，您可以看到它匯入兩個.targets 檔案。</span><span class="sxs-lookup"><span data-stu-id="5385c-117">If you take a look at the project file for a C#-based web application project, you can see that it imports two .targets files.</span></span>


[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample1.xml)]


<span data-ttu-id="5385c-118">第一個**匯入**陳述式是通用於所有 Visual C# 專案。</span><span class="sxs-lookup"><span data-stu-id="5385c-118">The first **Import** statement is common to all Visual C# projects.</span></span> <span data-ttu-id="5385c-119">這個檔案， *Microsoft.CSharp.targets*，包含目標和工作的特定 Visual C#。</span><span class="sxs-lookup"><span data-stu-id="5385c-119">This file, *Microsoft.CSharp.targets*, contains targets and tasks that are specific to Visual C#.</span></span> <span data-ttu-id="5385c-120">例如，C# 編譯器 (**Csc**) 這裡叫用工作。</span><span class="sxs-lookup"><span data-stu-id="5385c-120">For example, the C# compiler (**Csc**) task is invoked here.</span></span> <span data-ttu-id="5385c-121">*Microsoft.CSharp.targets*依次檔案匯入*Microsoft.Common.targets*檔案。</span><span class="sxs-lookup"><span data-stu-id="5385c-121">The *Microsoft.CSharp.targets* file in turn imports the *Microsoft.Common.targets* file.</span></span> <span data-ttu-id="5385c-122">這會定義目標通用於所有專案，例如**建置**，**重建**，**執行**，**編譯**，和**清除**.</span><span class="sxs-lookup"><span data-stu-id="5385c-122">This defines targets that are common to all projects, like **Build**, **Rebuild**, **Run**, **Compile**, and **Clean**.</span></span> <span data-ttu-id="5385c-123">第二個**匯入**陳述式是特定 web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="5385c-123">The second **Import** statement is specific to web application projects.</span></span> <span data-ttu-id="5385c-124">*Microsoft.WebApplication.targets*依次檔案匯入*Microsoft.Web.Publishing.targets*檔案。</span><span class="sxs-lookup"><span data-stu-id="5385c-124">The *Microsoft.WebApplication.targets* file in turn imports the *Microsoft.Web.Publishing.targets* file.</span></span> <span data-ttu-id="5385c-125">*Microsoft.Web.Publishing.targets*檔案基本上*是*WPP。</span><span class="sxs-lookup"><span data-stu-id="5385c-125">The *Microsoft.Web.Publishing.targets* file essentially *is* the WPP.</span></span> <span data-ttu-id="5385c-126">它會定義目標，例如**封裝**和**MSDeployPublish**，會叫用 Web Deploy 完成各種部署工作。</span><span class="sxs-lookup"><span data-stu-id="5385c-126">It defines targets, like **Package** and **MSDeployPublish**, that invoke Web Deploy to complete various deployment tasks.</span></span>

<span data-ttu-id="5385c-127">若要了解這些其他的目標中的使用方式，請連絡管理員範例方案中，開啟*Publish.proj*檔案，並看看**BuildProjects**目標。</span><span class="sxs-lookup"><span data-stu-id="5385c-127">To understand how these additional targets are used, in the Contact Manager sample solution, open the *Publish.proj* file and take a look at the **BuildProjects** target.</span></span>


[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample2.xml)]


<span data-ttu-id="5385c-128">這個目標會使用**MSBuild**來建立各種專案的工作。</span><span class="sxs-lookup"><span data-stu-id="5385c-128">This target uses the **MSBuild** task to build various projects.</span></span> <span data-ttu-id="5385c-129">請注意**DeployOnBuild**和**DeployTarget**屬性：</span><span class="sxs-lookup"><span data-stu-id="5385c-129">Notice the **DeployOnBuild** and **DeployTarget** properties:</span></span>

- <span data-ttu-id="5385c-130">**DeployOnBuild = true**屬性基本上是表示 「 我想要建置成功完成時執行的其他目標 」。</span><span class="sxs-lookup"><span data-stu-id="5385c-130">The **DeployOnBuild=true** property essentially means "I want to execute an additional target when build completes successfully."</span></span>
- <span data-ttu-id="5385c-131">**DeployTarget**屬性會識別您想要執行時的目標名稱**DeployOnBuild**屬性等於**true**。</span><span class="sxs-lookup"><span data-stu-id="5385c-131">The **DeployTarget** property identifies the name of the target you want to execute when the **DeployOnBuild** property is equal to **true**.</span></span> <span data-ttu-id="5385c-132">在此情況下，您會指定您想要執行 MSBuild**封裝**建置專案之後的目標。</span><span class="sxs-lookup"><span data-stu-id="5385c-132">In this case, you're specifying that you want MSBuild to execute the **Package** target after building the project.</span></span>

<span data-ttu-id="5385c-133">**封裝**中定義目標*Microsoft.Web.Publishing.targets*檔案。</span><span class="sxs-lookup"><span data-stu-id="5385c-133">The **Package** target is defined in the *Microsoft.Web.Publishing.targets* file.</span></span> <span data-ttu-id="5385c-134">基本上，此目標會採用您的 web 應用程式專案的建置輸出，並將它轉換成可以發行至 IIS web 伺服器的 web 部署封裝。</span><span class="sxs-lookup"><span data-stu-id="5385c-134">Essentially, this target takes the build output of your web application project and turns it into a web deployment package that can be published to an IIS web server.</span></span>

> [!NOTE]
> <span data-ttu-id="5385c-135">若要檢視的專案檔 (例如， *ContactManager.Mvc.csproj*) 在 Visual Studio 2010 中，您必須先卸載專案，從您的方案。</span><span class="sxs-lookup"><span data-stu-id="5385c-135">To view a project file (for example, *ContactManager.Mvc.csproj*) in Visual Studio 2010, you first need to unload the project from your solution.</span></span> <span data-ttu-id="5385c-136">在**方案總管 中**視窗中，以滑鼠右鍵按一下專案節點，然後**卸載專案**。</span><span class="sxs-lookup"><span data-stu-id="5385c-136">In the **Solution Explorer** window, right-click the project node, and then click **Unload Project**.</span></span> <span data-ttu-id="5385c-137">同樣地，以滑鼠右鍵按一下專案節點，然後按一下**編輯***[專案檔]*)。</span><span class="sxs-lookup"><span data-stu-id="5385c-137">Right-click the project node again, and then click **Edit***[project file]*).</span></span> <span data-ttu-id="5385c-138">未經處理的 XML 格式，將會開啟專案檔。</span><span class="sxs-lookup"><span data-stu-id="5385c-138">The project file will open in its raw XML form.</span></span> <span data-ttu-id="5385c-139">請記住，當您完成時重新載入專案。</span><span class="sxs-lookup"><span data-stu-id="5385c-139">Remember to reload the project when you're done.</span></span>  
> <span data-ttu-id="5385c-140">如需 MSBuild 目標，工作詳細資訊和**匯入**陳述式，請參閱[了解專案檔](understanding-the-project-file.md)。</span><span class="sxs-lookup"><span data-stu-id="5385c-140">For more information on MSBuild targets, tasks, and **Import** statements, see [Understanding the Project File](understanding-the-project-file.md).</span></span> <span data-ttu-id="5385c-141">專案檔和 WPP 的更深入簡介，請參閱[內 Microsoft Build Engine： 使用 MSBuild 和 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 和 William Bartholomew，ISBN: 978-0-7356-4524-0。</span><span class="sxs-lookup"><span data-stu-id="5385c-141">For a more in-depth introduction to project files and the WPP, see [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://amzn.com/0735645248) by Sayed Ibrahim Hashimi and William Bartholomew, ISBN: 978-0-7356-4524-0.</span></span>


## <a name="what-is-a-web-deployment-package"></a><span data-ttu-id="5385c-142">Web 部署套件為何？</span><span class="sxs-lookup"><span data-stu-id="5385c-142">What Is a Web Deployment Package?</span></span>

<span data-ttu-id="5385c-143">當您建置和部署 web 應用程式專案中，使用 Visual Studio 2010 或直接使用 MSBuild 時，最終結果通常是*web 部署套件*。</span><span class="sxs-lookup"><span data-stu-id="5385c-143">When you build and deploy a web application project, either by using Visual Studio 2010 or by using MSBuild directly, the end result is typically a *web deployment package*.</span></span> <span data-ttu-id="5385c-144">Web 部署封裝為.zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="5385c-144">The web deployment package is a .zip file.</span></span> <span data-ttu-id="5385c-145">它包含的所有項目 IIS 和 Web Deploy 才能重新建立您的 web 應用程式，包括：</span><span class="sxs-lookup"><span data-stu-id="5385c-145">It contains everything that IIS and Web Deploy need in order to recreate your web application, including:</span></span>

- <span data-ttu-id="5385c-146">Web 應用程式，包括內容、 資源檔、 組態檔、 JavaScript 和階層式樣式表 (CSS) 的資源，等編譯的輸出。</span><span class="sxs-lookup"><span data-stu-id="5385c-146">The compiled output of your web application, including content, resource files, configuration files, JavaScript and cascading style sheets (CSS) resources, and so on.</span></span>
- <span data-ttu-id="5385c-147">您的 web 應用程式專案和組件參考您的方案中的專案。</span><span class="sxs-lookup"><span data-stu-id="5385c-147">Assemblies for your web application project and for any referenced projects within your solution.</span></span>
- <span data-ttu-id="5385c-148">若要產生您要部署 web 應用程式的任何資料庫的 SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5385c-148">SQL scripts to generate any databases that you're deploying with your web application.</span></span>

<span data-ttu-id="5385c-149">之後產生的 web 部署套件之後，您可以將它發行至 IIS web 伺服器上以各種方式。</span><span class="sxs-lookup"><span data-stu-id="5385c-149">Once the web deployment package has been generated, you can publish it to an IIS web server in various ways.</span></span> <span data-ttu-id="5385c-150">例如，您可以將它部署從遠端將目標設為 Web 部署遠端代理程式服務或 Web 部署處理常式在目的地 web 伺服器上，或您可以使用 IIS 管理員以手動方式匯入目的地 web 伺服器上的套件。</span><span class="sxs-lookup"><span data-stu-id="5385c-150">For example, you can deploy it remotely by targeting the Web Deploy Remote Agent service or the Web Deploy Handler on the destination web server, or you can use IIS Manager to manually import the package on the destination web server.</span></span> <span data-ttu-id="5385c-151">如需有關部署這些方法的詳細資訊，請參閱[選擇 Web 部署的權限方法](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="5385c-151">For more information on these approaches to deployment, see [Choosing the Right Approach to Web Deployment](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md).</span></span>

## <a name="how-does-the-build-process-work"></a><span data-ttu-id="5385c-152">在建置程序的運作方式為何？</span><span class="sxs-lookup"><span data-stu-id="5385c-152">How Does the Build Process Work?</span></span>

<span data-ttu-id="5385c-153">以下會示範當您建置並封裝 web 應用程式專案時，會發生什麼情況：</span><span class="sxs-lookup"><span data-stu-id="5385c-153">This shows what happens when you build and package a web application project:</span></span>

![](building-and-packaging-web-application-projects/_static/image2.png)

<span data-ttu-id="5385c-154">當您建置的 web 應用程式專案時，建置程序會產生名為*[專案名稱]。SourceManifest.xml*。</span><span class="sxs-lookup"><span data-stu-id="5385c-154">When you build a web application project, the build process generates a file named *[project name].SourceManifest.xml*.</span></span> <span data-ttu-id="5385c-155">專案檔和組建輸出，以及這*。SourceManifest.xml*檔案會告知 Web Deploy 它需要包含 web 部署套件中。</span><span class="sxs-lookup"><span data-stu-id="5385c-155">Along with the project file and the build output, this *.SourceManifest.xml* file tells Web Deploy what it needs to include in the web deployment package.</span></span> <span data-ttu-id="5385c-156">這些輸入，使用 Web Deploy 會產生名為 web 部署套件*[專案名稱].zip*。</span><span class="sxs-lookup"><span data-stu-id="5385c-156">Using these inputs, Web Deploy generates a web deployment package named *[project name].zip*.</span></span>

<span data-ttu-id="5385c-157">Web 部署套件，以及建置程序會產生兩個檔案，可協助您使用的封裝：</span><span class="sxs-lookup"><span data-stu-id="5385c-157">Alongside the web deployment package, the build process generates two files that can help you to use the package:</span></span>

- <span data-ttu-id="5385c-158">*。 Deploy.cmd*檔案包含一組 web 部署套件發佈到遠端的 IIS 網頁伺服器的參數化 Web Deploy (MSDeploy.exe) 的命令。</span><span class="sxs-lookup"><span data-stu-id="5385c-158">The *.deploy.cmd* file includes a set of parameterized Web Deploy (MSDeploy.exe) commands that publish your web deployment package to a remote IIS web server.</span></span> <span data-ttu-id="5385c-159">執行*。 deploy.cmd*檔案，以適當的參數，通常會提供更快速和更容易替代來手動建構 MSDeploy.exe 命令自己。</span><span class="sxs-lookup"><span data-stu-id="5385c-159">Running the *.deploy.cmd* file, with appropriate parameters, typically provides a quicker and easier alternative to manually constructing the MSDeploy.exe commands yourself.</span></span>
- <span data-ttu-id="5385c-160">*SetParameters.xml*檔提供一組 MSDeploy.exe 命令的參數值。</span><span class="sxs-lookup"><span data-stu-id="5385c-160">The *SetParameters.xml* file provides a set of parameter values to the MSDeploy.exe command.</span></span> <span data-ttu-id="5385c-161">這些值包括如 IIS web 應用程式可供您想要部署封裝時，任何服務端點的值，但在中定義連接字串名稱屬性*web.config*檔和任何部署屬性在專案屬性頁上所定義的值。</span><span class="sxs-lookup"><span data-stu-id="5385c-161">These values include properties like the name of the IIS web application to which you want to deploy the package, the values of any service endpoints and connection strings defined in the *web.config* file, and any deployment property values defined on the project properties pages.</span></span>

<span data-ttu-id="5385c-162">*SetParameters.xml*檔案是管理部署程序的關鍵。</span><span class="sxs-lookup"><span data-stu-id="5385c-162">The *SetParameters.xml* file is key to managing the deployment process.</span></span> <span data-ttu-id="5385c-163">這個檔案是以動態方式產生，根據您的 web 應用程式專案的內容。</span><span class="sxs-lookup"><span data-stu-id="5385c-163">This file is generated dynamically according to the contents of your web application project.</span></span> <span data-ttu-id="5385c-164">例如，如果您加入連接字串，您*web.config*檔案，建置程序會自動偵測連接字串，因此，參數化部署並建立中的項目*SetParameters.xml*檔案，以讓您修改連接字串做為部署程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="5385c-164">For example, if you add a connection string to your *web.config* file, the build process will automatically detect the connection string, parameterize the deployment accordingly, and create an entry in the *SetParameters.xml* file to allow you to modify the connection string as part of the deployment process.</span></span> <span data-ttu-id="5385c-165">下一個主題[Web 封裝部署的設定參數](configuring-parameters-for-web-package-deployment.md)、 說明此檔案更詳細的角色，以及不同的方式，在其中您可以修改在建置和部署期間它。</span><span class="sxs-lookup"><span data-stu-id="5385c-165">The next topic, [Configuring Parameters for Web Package Deployment](configuring-parameters-for-web-package-deployment.md), explains the role of this file in more detail and describes the different ways in which you can modify it during build and deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="5385c-166">在 Visual Studio 2010、 WPP 不支援先行編譯封裝之前的 web 應用程式中的頁面。</span><span class="sxs-lookup"><span data-stu-id="5385c-166">In Visual Studio 2010, the WPP does not support precompiling the pages in a web application prior to packaging.</span></span> <span data-ttu-id="5385c-167">下一版的 Visual Studio 和 WPP 會包含先行編譯 web 應用程式做為封裝選項的能力。</span><span class="sxs-lookup"><span data-stu-id="5385c-167">The next version of Visual Studio and the WPP will include the ability to precompile a web application as a packaging option.</span></span>


## <a name="conclusion"></a><span data-ttu-id="5385c-168">結論</span><span class="sxs-lookup"><span data-stu-id="5385c-168">Conclusion</span></span>

<span data-ttu-id="5385c-169">本主題提供 Visual Studio 2010 中的 web 應用程式專案的建置和封裝程序的概觀。</span><span class="sxs-lookup"><span data-stu-id="5385c-169">This topic provided an overview of the build and packaging process for web application projects in Visual Studio 2010.</span></span> <span data-ttu-id="5385c-170">它說明如何 WPP 可讓您叫用 Web Deploy 命令從 MSBuild，和它說明如何建置和封裝程序運作。</span><span class="sxs-lookup"><span data-stu-id="5385c-170">It described how the WPP lets you invoke Web Deploy commands from MSBuild, and it explained how the build and packaging process works.</span></span>

<span data-ttu-id="5385c-171">建立 web 部署套件之後下, 一步是將其部署。</span><span class="sxs-lookup"><span data-stu-id="5385c-171">Once you've created a web deployment package, your next step is to deploy it.</span></span> <span data-ttu-id="5385c-172">如需詳細資訊，請參閱[Web 封裝部署的設定參數](configuring-parameters-for-web-package-deployment.md)和[部署 Web 封裝](deploying-web-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="5385c-172">For more information on this, see [Configuring Parameters for Web Package Deployment](configuring-parameters-for-web-package-deployment.md) and [Deploying Web Packages](deploying-web-packages.md).</span></span>

## <a name="further-reading"></a><span data-ttu-id="5385c-173">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="5385c-173">Further Reading</span></span>

<span data-ttu-id="5385c-174">在本教學課程中的下一個主題[Web 封裝部署的設定參數](configuring-parameters-for-web-package-deployment.md)和[部署 Web 封裝](deploying-web-packages.md)，提供如何使用您已建立此 web 封裝的指引。</span><span class="sxs-lookup"><span data-stu-id="5385c-174">The next topics in this tutorial, [Configuring Parameters for Web Package Deployment](configuring-parameters-for-web-package-deployment.md) and [Deploying Web Packages](deploying-web-packages.md), provide guidance on how to use the web package you've created.</span></span> <span data-ttu-id="5385c-175">在這一系列，最終的教學課程[進階企業 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)，提供有關如何自訂及疑難排解封裝程序指引。</span><span class="sxs-lookup"><span data-stu-id="5385c-175">The final tutorial in this series, [Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md), provides guidance on how to customize and troubleshoot the packaging process.</span></span>

<span data-ttu-id="5385c-176">專案檔和 WPP 的更深入簡介，請參閱[內 Microsoft Build Engine： 使用 MSBuild 和 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 和 William Bartholomew，ISBN: 978-0-7356-4524-0。</span><span class="sxs-lookup"><span data-stu-id="5385c-176">For a more in-depth introduction to project files and the WPP, see [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://amzn.com/0735645248) by Sayed Ibrahim Hashimi and William Bartholomew, ISBN: 978-0-7356-4524-0.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="5385c-177">[上一頁](understanding-the-build-process.md)
[下一頁](configuring-parameters-for-web-package-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="5385c-177">[Previous](understanding-the-build-process.md)
[Next](configuring-parameters-for-web-package-deployment.md)</span></span>