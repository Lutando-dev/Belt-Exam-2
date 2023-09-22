# Use the official Microsoft ASP.NET Core SDK as the build image
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env

# Set the ASPNETCORE_URLS environment variable
ENV ASPNETCORE_URLS=http://+:5104

# Set the working directory to /App
WORKDIR /App
EXPOSE 80

# Copy the .csproj files
COPY api/Basic3TierAPI/*.csproj ./Basic3TierAPI/
COPY api/Basic3Tier.Core/*.csproj ./Basic3Tier.Core/
COPY api/Basic3Tier.Infrastructure/*.csproj ./Basic3Tier.Infrastructure/

# Copy the solution file and restore NuGet packages
COPY api/Basic3TierAPI/Basic3TierAPI.sln ./Basic3TierAPI/
RUN dotnet restore Basic3TierAPI/Basic3TierAPI.sln

# Copy the rest of the source code
COPY api/Basic3TierAPI/. ./Basic3TierAPI/
COPY api/Basic3Tier.Core/. ./Basic3Tier.Core/
COPY api/Basic3Tier.Infrastructure/. ./Basic3Tier.Infrastructure/

# Build the application
RUN dotnet publish Basic3TierAPI/Basic3TierAPI.csproj -c Release -o out --no-cache /restore

# Build the final image using the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS runtime

# Set the working directory to /App
WORKDIR /App

# Copy the published output from build image
COPY --from=build-env /App/out .

# Set the entry point for the application
ENTRYPOINT ["dotnet", "Basic3TierAPI.dll"]
