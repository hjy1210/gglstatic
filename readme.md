## �ѦҸ��
* [Azure Static Web Apps documentation](https://learn.microsoft.com/en-us/azure/static-web-apps/) �� [Quickstart: Building your first static site with Azure Static Web Apps](https://learn.microsoft.com/en-us/azure/static-web-apps/getting-started?tabs=blazor)
* [Azure Static Web Apps documentation](https://learn.microsoft.com/en-us/azure/static-web-apps/) �� [Build an Azure Static Web Apps website with Blazor and serverless API](https://learn.microsoft.com/en-us/azure/static-web-apps/deploy-blazor)
* [Azure Static Web Apps �ҵ{](https://learn.microsoft.com/en-us/training/paths/azure-static-web-apps/) �� [Publish a Blazor WebAssembly app and .NET API with Azure Static Web Apps](https://learn.microsoft.com/en-us/training/modules/publish-app-service-static-web-app-api-dotnet/)

�ѦҤW�z�T���A�}�l�غc gglstatic ��סC
## �s�W gglstatic ��׻P Client �M��
* �s�W gglstatic ��סA�Ĥ@�ӱM�� Client: Blazor WebAssembly(.Net 6.0) �M��
* �Ѧ� [Publish a Blazor WebAssembly app and .NET API with Azure Static Web Apps](https://learn.microsoft.com/en-us/training/modules/publish-app-service-static-web-app-api-dotnet/) �[�J Azure Static Web App workflow(Azure Portal)

## �[�J Shared
* �[�J���O�w�M�� Shared(.Net Standard 2.0)
    * �[�J WeatherForecast ���O�A�� Client �P Api �M�׳��i�H�ϥΡC
## �[�J Api
* �[�J Azure functions �M�� Api(.Net 6.0(LTS))
    * launchSettings.json>profiles.Api.commandLineArgs ���ȥ� "--port 7199" �令 "start --cors * --port 7199"(��Client�@�I�s Api �ɨS��CORS���D)
    * �[�J Azure ��� Function1 �P WeatherForecastFunction

## Client �I�s Api
* Client.wwwroot.appsettings.Development.json �̭��] "API_Prefix": "http://localhost:7199"�A��local�ݰ���ɪ��D�p��I�sApi�C
* Client.Program.cs �̭��A`BaseAddress = new Uri(builder.HostEnvironment.BaseAddress)`�令`BaseAddress = new Uri(builder.Configuration["API_Prefix"] ?? builder.HostEnvironment.BaseAddress)`�A��cloacal�}�o�P���ݧG�خɳ���o�q�C
* Client �̭��s�Wrazor ���� CallFunction1,razor�A�̭��I�s Api �� Function1
* Client �� Index.razor �ϥΤF CallFunction1,razor
* Client �� FetchData.razor �����A�ק令�I�s Api �� WeatherForecastFunction�C

ĵ�i: �i�H�����s����Api�h�A�Ҧp https://......azurestaticapps.net/api/WeatherForecastFunction�A�ҥH�w���ʻݭn�[�j�C�i�Ѧ� [Authenticate Blazor WebAssembly with Azure Static Web Apps](https://anthonychu.ca/post/blazor-auth-azure-static-web-apps/#:~:text=To%20set%20up%20a%20Blazor,the%20logged%20in%20user's%20identity)