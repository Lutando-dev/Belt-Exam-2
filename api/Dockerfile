# Use the official Microsoft ASP.NET Core runtime image
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

# Use the official Microsoft ASP.NET Core SDK as the build image
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["api/Basic3TierAPI/Basic3TierAPI.csproj", "Basic3TierAPI/"]
RUN dotnet restore "api/Basic3TierAPI/Basic3TierAPI.csproj"
COPY . .
WORKDIR "/src/Basic3TierAPI"
RUN dotnet build "Basic3TierAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Basic3TierAPI.csproj" -c Release -o /app/publish

# Build the final image using the runtime image
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Basic3TierAPI.dll"]
