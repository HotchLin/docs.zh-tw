---
title: "使用 Microsoft 工具的 Docker 應用程式 devops 工作流程"
description: "Microsoft 平台和工具的容器化 Docker 應用程式生命週期，使用 Microsoft 工具的 devops 工作流程"
keywords: "Docker, 微服務, ASP.NET, 容器"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/22/2017
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 8539e8c0a6d0c6c9d558b91e062184e7ef135856
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/23/2017
---
# <a name="docker-application-devops-workflow-with-microsoft-tools"></a>使用 Microsoft 工具的 Docker 應用程式 DevOps 工作流程

Microsoft Visual Studio、Visual Studio Team Services、Team Foundation Server 和 Application Insights 提供完整的生態系統進行開發和 IT 作業，可讓您的小組管理專案以及快速建置、測試和部署容器化應用程式。

在雲端中使用 Visual Studio 和 Visual Studio Team Services，以及在內部部署環境中使用 Team Foundation Server，開發小組就可以有效率地建置、測試和發行導向任何平台 (Windows 或 Linux) 的容器化應用程式。

Microsoft 工具可以自動化特定容器化應用程式實作的管線 (Docker、.NET Core 或與其他平台的任意組合)，範圍從全域組建和持續整合 (CI) 並使用 Visual Studio Team Services 或 Team Foundation Server 的測試，到持續部署 (CD) 到 Docker 環境 (開發、準備、生產)，以及透過 Application Insights 將服務的分析資訊傳輸至開發小組。 每個程式碼認可都可以啟始建置 (CI)，並將服務自動部署至特定容器化環境 (CD)。

開發人員和測試人員可以使用 Microsoft Azure 中的範本，以根據 Docker 輕鬆且快速地佈建類似生產環境的開發和測試環境。

根據商務複雜性和延展性需求，容器化應用程式開發的複雜度會穩定增加。 這個的不錯範例是根據微服務架構的應用程式。 若要在這類環境中成功，您的專案必須自動化整個生命週期：不僅建置和部署，也必須管理版本和遙測集合。 Visual Studio Team Services 和 Azure 提供下列功能：

-   Visual Studio Team Services/Team Foundation Server 原始程式碼管理 (根據 Git 或 Team Foundation 版本控制)、Agile 規劃 (支援 Agile、Scrum 和 CMMI)、CI、發行管理，以及 Agile 小組的其他工具。

-   Visual Studio Team Services/Team Foundation Server 包含功能強大且不斷成長的生態系統，而您可以使用其第一方和第三方延伸模組輕鬆地建構微服務的 CI、建置、測試、傳遞和發行管理管線。

-   在 Visual Studio Team Services 中，於組建管線期間執行自動化測試。

-   Visual Studio Team Services 可以利用傳遞至多個環境來加強 DevOps 生命週期，不只是傳遞至生產環境，也傳遞至測試環境 (包含 A/B 實驗、[anary 發行](http://martinfowler.com/bliki/CanaryRelease.html)等等)。

-   組織可以搭配使用 Azure Resource Manager 範本與他們已用來輕鬆執行的工具，以從 Azure Container Registry 中所儲存的私人映像以及與 Azure 元件 (Data、PaaS 等等) 的任何相依性來輕鬆地佈建 Docker 容器。


>[!div class="step-by-step"]
[上一個] (../design-develop-containerized-apps/set-up-windows-containers-with-powershell.md) [下一個] (docker-application-outer-loop-devops-workflow.md)
