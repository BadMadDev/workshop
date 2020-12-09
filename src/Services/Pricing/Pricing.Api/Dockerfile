FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src

COPY "ServicesAndWebApps.sln" "ServicesAndWebApps.sln"

COPY "docker-compose.dcproj" "docker-compose.dcproj"

COPY "Services/Pricing/Pricing.Api/Pricing.Api.csproj" "Services/Pricing/Pricing.Api/Pricing.Api.csproj"

RUN dotnet restore "ServicesAndWebApps.sln"

COPY . .
WORKDIR /src/Services/Pricing/Pricing.Api
RUN dotnet publish --no-restore -c Release -o /app

FROM build AS publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Pricing.Api.dll"]