FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

COPY ["src/PublicApi/", "/src/PublicApi/"]
COPY ["src/ApplicationCore/", "/src/ApplicationCore/"]
COPY ["src/BlazorShared/", "/src/BlazorShared/"]
COPY ["src/BlazorAdmin/", "/src/BlazorAdmin/"]
COPY ["src/Infrastructure/", "/src/Infrastructure/"]
COPY Directory.Packages.props ./

RUN dotnet publish "/src/PublicApi/PublicApi.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
USER app

COPY --from=build /app/publish .

ENTRYPOINT ["dotnet", "PublicApi.dll"]