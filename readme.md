* Client: Blazor WebAssembly(.Net 6.0)
* �[�J Azure Static Web App workflow(Azure Portal)

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
