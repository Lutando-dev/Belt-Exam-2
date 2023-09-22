FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

WORKDIR /App

COPY ["api/Basic3TierAPI/Basic3TierAPI.csproj", "Basic3TierAPI/"]
COPY ["api/Basic3Tier.Core/Basic3Tier.Core.csproj", "Basic3Tier.Core/"]
COPY ["api/Basic3Tier.Infrastructure/Basic3Tier.Infrastructure.csproj", "Basic3Tier.Infrastructure/"]

RUN dotnet restore Basic3Tier.Core/Basic3Tier.Core.csproj
RUN dotnet build Basic3Tier.Core/Basic3Tier.Core.csproj -c Release -o out

RUN dotnet restore Basic3Tier.Infrastructure/Basic3Tier.Infrastructure.csproj
RUN dotnet build Basic3Tier.Infrastructure/Basic3Tier.Infrastructure.csproj -c Release -o out

RUN dotnet restore Basic3TierAPI/Basic3TierAPI.csproj
RUN dotnet build Basic3TierAPI/Basic3TierAPI.csproj -c Release -o out

FROM mcr.microsoft.com/dotnet/runtime:7.0

WORKDIR /App

COPY --from=build /App/out/ ./

ENTRYPOINT ["dotnet", "Basic3TierAPI.dll"]
