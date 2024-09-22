FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

COPY ["src/Web/Web.csproj", "/src/Web/"]
COPY ["src/ApplicationCore/ApplicationCore.csproj", "/src/ApplicationCore/"]
COPY ["src/BlazorShared/BlazorShared.csproj", "/src/BlazorShared/"]
COPY ["src/BlazorAdmin/BlazorAdmin.csproj", "/src/BlazorAdmin/"]
COPY ["src/Infrastructure/Infrastructure.csproj", "/src/Infrastructure/"]
COPY Directory.Packages.props ./

RUN dotnet restore "/src/Web/Web.csproj"

COPY . .

RUN dotnet build "/src/Web/Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "/src/Web/Web.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
USER app
WORKDIR /app

COPY --from=publish /app/publish .

ENTRYPOINT ["dotnet", "Web.dll"]