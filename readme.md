* Client: Blazor WebAssembly(.Net 6.0)
* 加入 Azure Static Web App workflow(Azure Portal)

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
