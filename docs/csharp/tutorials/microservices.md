---
title: "在 Docker 中裝載的微服務 - C#"
description: "了解如何建立在 Docker 容器中執行的 ASP.NET Core 服務"
keywords: ".NET, .NET Core, Docker, C#, ASP.NET, 微服務"
author: BillWagner
ms.author: wiwagn
ms.date: 02/03/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-docker
ms.devlang: csharp
ms.assetid: 87e93838-a363-4813-b859-7356023d98ed
ms.openlocfilehash: d399cdce81350356b71e21d879a4f5b5079f98d8
ms.sourcegitcommit: 2142a4732bb4ff519b9817db4c24a237b9810d4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="microservices-hosted-in-docker"></a>在 Docker 中裝載的微服務

本教學課程詳細說明在 Docker 容器中建置和部署 ASP.NET Core 微服務所需的工作。 您將在本教學課程中了解︰

* 如何使用 Yeoman 產生 ASP.NET Core 應用程式
* 如何建立開發 Docker 的環境
* 如何根據現有的映像來建立 Docker 映像。
* 如何將您的服務部署到 Docker 容器中。

您也會在本教學課程當中看到一些 C# 語言功能︰

* 如何將 C# 物件轉換成 JSON 裝載。
* 如何建置不可變的資料傳輸物件
* 如何處理傳入 HTTP 要求和產生 HTTP 回應
* 如何使用可為 Null 的實值型別

您可以[檢視或下載本主題的範例應用程式 (英文)](https://github.com/dotnet/docs/tree/master/samples/csharp/getting-started/WeatherMicroservice)。 如需下載指示，請參閱[範例和教學課程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)。

### <a name="why-docker"></a>為何要使用 Docker？

Docker 可讓您輕鬆地建立標準的機器映像，在資料中心或公用雲端裝載您的服務。 Docker 可讓您設定映像，並視需要複製來調整應用程式的安裝。

本教學課程中的所有程式碼可在任何 .NET Core 環境中運作。
Docker 安裝的其他工作均適用於 ASP.NET Core 應用程式。 

## <a name="prerequisites"></a>必要條件
您必須設定電腦以執行 .NET Core。 您可以在 [.NET Core (英文)](https://www.microsoft.com/net/core) 頁面找到安裝指示。
您可以在 Windows、Ubuntu Linux、macOS 或是 Docker 容器中執行此應用程式。 您將必須安裝慣用的程式碼編輯器。 以下說明使用 [Visual Studio Code (英文)](https://code.visualstudio.com/)，這是開放原始碼的跨平台編輯器。 不過，您可以使用您熟悉的任何工具。

您也需要安裝 Docker 引擎。 如需適用於您平台的指示，請參閱 [Docker 安裝頁面 (英文)](http://www.docker.com/products/docker)。
Docker 可以安裝在許多 Linux 發行版本、macOS 或 Windows。 上述的參考頁面包含每個可用安裝的相關章節。

大部分元件都是由封裝管理員來安裝。 如果您已安裝 node.js 的封裝管理員 `npm`，可以略過此步驟。 否則，請從 [nodejs.org](https://nodejs.org) 安裝最新的 NodeJs ，以安裝 npm 封裝管理員。 

此時，您必須安裝一些支援 ASP.NET Core 開發的命令列工具。 命令列範本使用 Yeoman、Bower、Grunt 及 Gulp。 如果您已經安裝上述工具就已準備就緒，否則請將下列命令輸入到您慣用的殼層：

`npm install -g yo bower grunt-cli gulp`

`-g` 選項指出它是全域安裝，而且可在全系統使用這些工具。 (封裝的本機安裝範圍為單一專案)。 在您安裝這些核心工具之後，您必須安裝 Yeoman ASP.NET 範本產生器︰

`npm install -g generator-aspnet`

## <a name="create-the-application"></a>建立應用程式

現在您已安裝完所有工具，請建立新的 ASP.NET Core 應用程式。 若要使用命令列產生器，請在您慣用的殼層中執行下列 Yeoman 命令︰

`yo aspnet`

此命令會提示您選取想要建立哪種類型的應用程式。 對於這個微服務，需要有盡可能簡單且最為輕量的 Web 應用程式，因此選取 [空白 Web 應用程式]。 範本會提示您輸入一個名稱。 選取 [WeatherMicroservice]。 

這個範本會為您建立八個檔案︰

* .gitignore，自訂的 ASP.NET Core 應用程式。
* Startup.cs 檔案。 這當中包含應用程式的基礎。
* Program.cs 檔案。 這當中包含應用程式的進入點。
* WeatherMicroservice.csproj 檔案。 這是應用程式的組建檔案。
* Dockerfile。 此指令碼會建立應用程式的 Docker 映像。
* README.md。 這包含其他 ASP.NET Core 資源的連結。
* web.config 檔案。 這包含基本組態資訊。
* runtimeconfig.template.json 檔案。 這包含 IDE 所使用的偵錯設定。

現在，您可以執行範本產生的應用程式。 這是從命令列使用一系列工具來完成。 `dotnet` 命令會執行 .NET 開發所需的工具。 每個動詞都會執行不同的命令

第一步是還原所有相依性︰

```console
dotnet restore
```

Dotnet restore 會使用 NuGet 封裝管理員，將所有必要的封裝安裝到應用程式目錄。 它也會產生 project.json.lock 檔案。 這個檔案包含所參考之每個封裝的相關資訊。 在還原所有相依性之後，您就可以建置應用程式︰

```console
dotnet build
```
[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

然後在您建置應用程式之後，可以從命令列來執行它︰

```console
dotnet run
```

預設組態會接聽 http://localhost:5000 。 您可以開啟瀏覽器，然後瀏覽至該頁面，就會看到「Hello World!」 訊息。

### <a name="anatomy-of-an-aspnet-core-application"></a>ASP.NET Core 應用程式的結構

既然您已經建置應用程式，現在讓我們來看看如何實作這項功能。 此時，產生的檔案當中有兩個特別有趣︰project.json 和 Startup.cs。 

Project.json 包含該專案的相關資訊。 您會經常使用的兩個節點為「相依性」和「架構」。 相依性節點會列出此應用程式所需的所有封裝。
目前，這是一個小型節點，只需要執行 Web 伺服器的封裝。

「架構」節點會指定將執行此應用程式的 .NET Framework 版本和組態。

在 Startup.cs 中實作應用程式。 此檔案包含啟動類別。

ASP.NET Core 基礎結構會呼叫這兩個方法，來設定和執行應用程式。 `ConfigureServices` 方法描述此應用程式所需的服務。 您正在建置精簡的微服務，因此它不需要設定任何相依性。 `Configure` 方法會設定傳入 HTTP 要求的處理常式。 範本會產生能以「Hello World!」文字回應任何要求的簡單處理常式。

## <a name="build-a-microservice"></a>建置微服務

您即將建置的服務可提供世界上任何地方的氣象報告。 在實際執行應用程式中，您會呼叫某些服務來擷取氣象資料。 對我們的範例而言，則將會產生隨機的氣象預報。 

您必須執行數項工作，才能實作隨機的氣象服務︰

* 剖析傳入要求以讀取緯度和經度。
* 產生一些隨機的預測資料。
* 將隨機的預測資料從 C# 物件轉換為 JSON 封包。
* 設定回應標頭，指出您的服務會傳送回 JSON。
* 撰寫回應。

下一節將逐步說明每一個步驟。

### <a name="parsing-the-query-string"></a>剖析查詢字串。

一開始要先剖析查詢字串。 服務會接受下列格式查詢字串的 'lat' 和 'long' 引數：

`http://localhost:5000/?lat=-35.55&long=-12.35`  

您需要的所有變更都是針對啟動類別中的 `app.Run` 定義為引數的 Lambda 運算式中進行。

Lambda 運算式中的引數就是要求的 `HttpContext`。 它的其中一個屬性是 `Request` 物件。 `Request` 物件具有 `Query` 屬性，其中包含要求的查詢字串上所有值的字典。 首先要加入的內容是尋找緯度和經度值︰

[!code-csharp[ReadQueryString](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#ReadQueryString "read variables from the query string")]

查詢字典值為 `StringValue` 型別。 該型別可以包含字串集合。 對於氣象服務而言，每個值都是單一字串。 這就是在上述程式碼中呼叫 `FirstOrDefault()` 的原因。 

接著，您必須將字串轉換為雙精度浮點數。 您用來將字串轉換為雙精度浮點數的方法是 `double.TryParse()`：

```csharp
bool TryParse(string s, out double result);
```

此方法會利用 C# 的輸出參數，指出該輸入字串是否能轉換為雙精度浮點數。 如果字串的確是有效的雙精度浮點數表示法，該方法會傳回 true，`result` 引數也會包含值。 如果字串不代表有效的雙精度浮點數，則該方法會傳回 false。

您可以採用該 API 搭配使用「擴充方法」，來傳回「可為 Null 的雙精度浮點數」。 「可為 Null 的實值型別」是代表一些實值型別的一種型別，它也可以保留遺漏值或 Null 值。 在型別宣告附加 `?` 字元，即表示它是可為 Null 的型別。 

擴充方法是指定義為靜態方法，但在第一個參數加上 `this` 修飾詞的方法，可以如同是該類別的成員一般來呼叫。 擴充方法只能在靜態類別中定義。 以下的類別定義包含可用於剖析的擴充方法：

[!code-csharp[TryParseExtension](../../../samples/csharp/getting-started/WeatherMicroservice/Extensions.cs#TryParseExtension "try parse to a nullable")]

`default(double?)` 運算式會傳回 `double?` 型別的預設值。 該預設值是 Null (或遺漏) 值。

您可以使用此擴充方法，將查詢字串引數轉換成 double 型別︰

[!code-csharp[UseTryParse](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#UseTryParse "Use the try parse extension method")]

更新回應以包含該引數的值，即可輕鬆地測試剖析程式碼︰

[!code-csharp[WriteResponse](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#WriteResponse "Write the output response")]

此時，您可以執行 Web 應用程式，並查看您的剖析程式碼是否可以正常運作。 將值加入至瀏覽器中的 Web 要求後，您應該會看到更新的結果。

### <a name="build-a-random-weather-forecast"></a>建立隨機的氣象預報

您的下一個工作是建立隨機的氣象預報。 讓我們從保存您所想要氣象預報值的資料容器開始︰

```csharp
public class WeatherReport
{
    private static readonly string[] PossibleConditions = new string[]
    {
        "Sunny",
        "Mostly Sunny",
        "Partly Sunny",
        "Partly Cloudy",
        "Mostly Cloudy",
        "Rain"
    };

    public int HiTemperature { get; }
    public int LoTemperature { get; }
    public int AverageWindSpeed { get; }
    public string Conditions { get; }
}
```

接下來，建置會隨機設定這些值的建構函式。 此建構函式會使用經度和緯度的值來植入亂數產生器。 這表示相同位置會有相同的預報。 如果您變更緯度和經度的引數，您會得到不同的預報 (因為您從不同的種子開始)。

[!code-csharp[WeatherReportConstructor](../../../samples/csharp/getting-started/WeatherMicroservice/WeatherReport.cs#WeatherReportConstructor "Weather Report Constructor")]

您現在能以您的回應方法產生 5 天的預報︰

[!code-csharp[GenerateRandomReport](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#GenerateRandomReport "Generate a random weather report")]

### <a name="build-the-json-response"></a>建立 JSON 回應。

伺服器上最後的程式碼工作是將 WeatherReport 陣列轉換為 JSON 封包，並傳送回用戶端。 現在就開始建立 JSON 封包。 您要將 NewtonSoft JSON 序列化程式加入至相依性清單。 您可以使用 `dotnet` CLI 來完成：

```
dotnet add package Newtonsoft.Json
```

然後，您可以使用 `JsonConvert` 類別來將該物件撰寫為字串︰

[!code-csharp[ConvertToJson](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#ConvertToJSON "Convert objects to JSON")]

上述程式碼會將預報物件 (`WeatherForecast` 物件清單) 轉換為 JSON 封包。 在您完成建構回應封包之後，您可以將內容類型設定為 `application/json`，然後撰寫字串。

應用程式現在會執行，並傳回隨機的預測。

## <a name="build-a-docker-image"></a>建置 Docker 映像

最後一項工作是在 Docker 中執行應用程式。 我們會建立 Docker 容器，執行代表應用程式的 Docker 映像。

「Docker 映像」這個檔案會定義用來執行應用程式的環境。

「Docker 容器」代表 Docker 映像的執行中執行個體。

比方說，您可以將「Docker 映像」視為「類別」，而將「Docker 容器」視為物件，或該類別的執行個體。  

針對本文的目的，很適合使用 ASP.NET 範本所建立的 Dockerfile。 讓我們來看看它的內容。

第一行會指定來源映像︰

```
FROM microsoft/dotnet:1.1-sdk-msbuild
```

Docker 可讓您根據來源範本來設定機器映像。 這表示當您啟動時，不需要提供所有的機器參數，您只需要提供所做的任何變更。 此處的變更會包含在我們的應用程式中。

在這個第一個範例中，我們將使用 `1.1-sdk-msbuild` 版的 DotNet 映像。 這是建立 Docker 工作環境的最簡單方式。 此映像包含 DotNet Core 執行階段和 DotNet SDK。 那樣可以更容易開始使用和建置，但會建立較大的映象。

接下來的五行會安裝並建置您的應用程式︰

```
WORKDIR /app

# copy csproj and restore as distinct layers

COPY WeatherMicroservice.csproj .
RUN dotnet restore 

# copy and build everything else

COPY . .

# RUN dotnet restore
RUN dotnet publish -c Release -o out
```

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

這會將目前目錄中的專案檔案複製到 Docker VM，並還原所有套件。 使用 DotNet CLI，表示 Docker 映像必須包含 .NET Core SDK。 之後，會複製您應用程式其餘的部分，然後 dotnet publish 命令會建置和封裝您的應用程式。

此檔案的最後一行會執行該應用程式︰

```
ENTRYPOINT ["dotnet", "out/WeatherMicroservice.dll", "--server.urls", "http://0.0.0.0:5000"]
```

此設定的連接埠是參考 Dockerfile 最後一行 `dotnet` 的 `--server.urls` 引數。 `ENTRYPOINT` 命令會通知 Docker 哪些命令和命令列選項啟動該服務。 

## <a name="building-and-running-the-image-in-a-container"></a>建置和執行容器中的映像。

讓我們在 Docker 容器內建置映像並執行服務。 不建議將本機目錄中的所有檔案複製到映像中。 相反地，您要在容器中建置應用程式。 您會建立 `.dockerignore` 檔案，以指定不要複製到映像中的目錄。 不建議複製任何的組建資產。 請在 `.dockerignore` 檔案中指定組建和發行目錄：

```
bin/*
obj/*
out/*
```

您會使用 `docker build` 命令來建置映像。 從包含您程式碼的目錄執行下列命令。

```console
docker build -t weather-microservice .
```

此命令會根據 Dockerfile 中的所有資訊來建置容器映像。 `-t` 引數會提供此容器映像的標籤或名稱。 在上述命令列中，Docker 容器所使用的標籤是 `weather-microservice`。 此命令完成時，容器已準備好可以執行新的服務。 

執行下列命令以啟動容器並啟動您的服務︰

```console
docker run -d -p 80:5000 --name hello-docker weather-microservice
```

`-d` 選項表示要執行和目前終端機中斷連結的容器。 這表示您不會在終端機看到命令輸出。 `-p` 選項會指出服務和主機之間的連接埠對應。 這裡指出連接埠 80 上的任何傳入要求都應該轉送到容器上的連接埠 5000。 使用 5000 才會符合您的服務正在從上述 Dockerfile 中指定的命令列引數接聽的連接埠。 `--name` 引數會命名執行中的容器。 該名稱可方便您使用該容器。 

您可以透過檢查以下命令，來查看映像是否正在執行︰

```console
docker ps
```

如果您的容器正在執行中，您會在執行中處理序看到當中有一行將它列出。 (它可能是唯一的一行)。

開啟瀏覽器並瀏覽到 localhost，然後指定緯度和經度來測試您的服務︰

```
http://localhost/?lat=35.5&long=40.75
```

## <a name="attaching-to-a-running-container"></a>附加至執行中的容器

當您在命令視窗中執行服務時，您可以看到為每個要求印出的診斷資訊。 當您的容器在中斷連結模式中執行時，您看不到該資訊。 Docker attach 命令可讓您附加至執行中的容器，以便查看記錄資訊。  請從命令視窗執行這個命令︰

```console
docker attach --sig-proxy=false hello-docker
```

`--sig-proxy=false` 引數表示不會將 `Ctrl-C` 命令傳送到此容器處理序，但會停止 `docker attach` 命令。 最後一個引數是要在 `docker run` 命令中提供給容器的名稱。 

> [!NOTE]
> 您也可以使用 Docker 指派的容器識別碼來參考任何容器。 如果您並未在 `docker run` 中為您的容器指定名稱 ，您必須使用容器的 ID。

開啟瀏覽器，並瀏覽到您的服務。 您會在命令視窗中看到來自所附加執行中容器的診斷訊息。

按下 `Ctrl-C` 可停止附加處理序。

當您完成使用容器，可以將它停止︰

```console
docker stop hello-docker
```

您仍然可以重新啟動該容器和映像。  如果您想要從機器中移除該容器，您可以使用此命令︰

```console
docker rm hello-docker
```

如果您想要從機器中移除未使用的映像，您可以使用此命令︰

```console
docker rmi weather-microservice
```

## <a name="conclusion"></a>結論 

在本教學課程中，您已建置 ASP.NET Core 微服務，並新增一些簡單的功能。

您為該服務建置了 Docker 容器映像，並在您的機器上執行該容器。 您將終端機視窗附加至該服務，並看到來自您服務的診斷訊息。

過程中，您也看到一些 C# 語言功能的實際運作。
