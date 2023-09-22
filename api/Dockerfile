FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

WORKDIR /App

COPY *.sln .
COPY ["api/Basic3TierAPI/Basic3TierAPI.csproj", "./Basic3TierAPI/"]
COPY ["api/Basic3Tier.Core/Basic3Tier.Core.csproj", "./Basic3Tier.Core/"]
COPY ["api/Basic3Tier.Infrastructure/Basic3Tier.Infrastructure.csproj", "./Basic3Tier.Infrastructure/"]

RUN dotnet restore
#
# copy everything else and build app
COPY ["api/Basic3TierAPI/.", "./Basic3TierAPI/"]
COPY ["api/Basic3Tier.Core/.", "./Basic3Tier.Core/"]
COPY ["api/Basic3Tier.Infrastructure/.", "./Basic3Tier.Infrastructure/"]

WORKDIR /App/Experiment
RUN dotnet publish -c Release -o out 

FROM mcr.microsoft.com/dotnet/runtime:7.0
WORKDIR /App

COPY --from=build /App/Experiment/out/ ./

ENTRYPOINT ["dotnet", "Basic3TierAPI.dll"]
