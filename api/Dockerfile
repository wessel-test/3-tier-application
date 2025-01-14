FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src

# Copy csproj files first for caching purposes
COPY ["api/Basic3TierAPI/Basic3TierAPI.csproj", "Basic3TierAPI/"]
COPY ["api/Basic3Tier.Core/Basic3Tier.Core.csproj", "Basic3Tier.Core/"]
COPY ["api/Basic3Tier.Infrastructure/Basic3Tier.Infrastructure.csproj", "Basic3Tier.Infrastructure/"]

# Restore as distinct layers
RUN dotnet restore "Basic3TierAPI/Basic3TierAPI.csproj"

# Copy everything else and build
COPY ./api/. ./api/

WORKDIR "/src/api/Basic3TierAPI"

RUN dotnet build "Basic3TierAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Basic3TierAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .

ENTRYPOINT ["dotnet", "Basic3TierAPI.dll"]
