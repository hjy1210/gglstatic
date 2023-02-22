## 參考資料
* [Azure Static Web Apps documentation](https://learn.microsoft.com/en-us/azure/static-web-apps/) 的 [Quickstart: Building your first static site with Azure Static Web Apps](https://learn.microsoft.com/en-us/azure/static-web-apps/getting-started?tabs=blazor)
* [Azure Static Web Apps documentation](https://learn.microsoft.com/en-us/azure/static-web-apps/) 的 [Build an Azure Static Web Apps website with Blazor and serverless API](https://learn.microsoft.com/en-us/azure/static-web-apps/deploy-blazor)
* [Azure Static Web Apps 課程](https://learn.microsoft.com/en-us/training/paths/azure-static-web-apps/) 的 [Publish a Blazor WebAssembly app and .NET API with Azure Static Web Apps](https://learn.microsoft.com/en-us/training/modules/publish-app-service-static-web-app-api-dotnet/)

參考上述三文件，開始建構 gglstatic 方案。
## 新增 gglstatic 方案與 Client 專案
* 新增 gglstatic 方案，第一個專案 Client: Blazor WebAssembly(.Net 6.0) 專案
* 參考 [Publish a Blazor WebAssembly app and .NET API with Azure Static Web Apps](https://learn.microsoft.com/en-us/training/modules/publish-app-service-static-web-app-api-dotnet/) 加入 Azure Static Web App workflow(Azure Portal)

## 加入 Shared
* 加入類別庫專案 Shared(.Net Standard 2.0)
    * 加入 WeatherForecast 類別，讓 Client 與 Api 專案都可以使用。
## 加入 Api
* 加入 Azure functions 專案 Api(.Net 6.0(LTS))
    * launchSettings.json>profiles.Api.commandLineArgs 的值由 "--port 7199" 改成 "start --cors * --port 7199"(讓Client　呼叫 Api 時沒有CORS問題)
    * 加入 Azure 函數 Function1 與 WeatherForecastFunction

## Client 呼叫 Api
* Client.wwwroot.appsettings.Development.json 裡面設 "API_Prefix": "http://localhost:7199"，讓local端執行時知道如何呼叫Api。
* Client.Program.cs 裡面，`BaseAddress = new Uri(builder.HostEnvironment.BaseAddress)`改成`BaseAddress = new Uri(builder.Configuration["API_Prefix"] ?? builder.HostEnvironment.BaseAddress)`，讓cloacal開發與雲端佈建時都行得通。
* Client 裡面新增razor 元件 CallFunction1,razor，裡面呼叫 Api 的 Function1
* Client 的 Index.razor 使用了 CallFunction1,razor
* Client 的 FetchData.razor 頁面，修改成呼叫 Api 的 WeatherForecastFunction。

警告: 可以直接瀏覽到Api去，例如 https://......azurestaticapps.net/api/WeatherForecastFunction，所以安全性需要加強。可參考 [Authenticate Blazor WebAssembly with Azure Static Web Apps](https://anthonychu.ca/post/blazor-auth-azure-static-web-apps/#:~:text=To%20set%20up%20a%20Blazor,the%20logged%20in%20user's%20identity)