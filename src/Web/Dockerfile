FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

COPY ["src/Web/", "/src/Web/"]
COPY ["src/ApplicationCore/", "/src/ApplicationCore/"]
COPY ["src/BlazorShared/", "/src/BlazorShared/"]
COPY ["src/BlazorAdmin/", "/src/BlazorAdmin/"]
COPY ["src/Infrastructure/", "/src/Infrastructure/"]
COPY Directory.Packages.props ./

RUN dotnet restore "/src/Web/Web.csproj"

RUN dotnet publish "/src/Web/Web.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
USER app

COPY --from=build /app/publish .

ENTRYPOINT ["dotnet", "Web.dll"]