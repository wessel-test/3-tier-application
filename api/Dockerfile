# Use the .NET SDK image for building the application
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

# Set the working directory inside the container
WORKDIR /src

# Copy the .csproj files and restore dependencies
COPY ["Basic3TierAPI/Basic3TierAPI.csproj", "Basic3TierAPI/"]
COPY ["Basic3Tier.Core/Basic3Tier.Core.csproj", "Basic3Tier.Core/"]
COPY ["Basic3Tier.Infrastructure/Basic3Tier.Infrastructure.csproj", "Basic3Tier.Infrastructure/"]

# Restore as distinct layers
RUN dotnet restore "Basic3TierAPI/Basic3TierAPI.csproj"

# Copy the entire source code into the container
COPY . .

# Set the working directory for building the application
WORKDIR "/src/Basic3TierAPI"

# Build the application
RUN dotnet build "Basic3TierAPI.csproj" -c Release -o /app/build

# Publish the application
FROM build AS publish
RUN dotnet publish "Basic3TierAPI.csproj" -c Release -o /app/publish

# Use the ASP.NET runtime image for running the application
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS final

# Set the working directory in the final image
WORKDIR /app

# Copy the published output from the previous stage
COPY --from=publish /app/publish .

# Expose port 80 (or any other port your application uses)
EXPOSE 80

# Define the entry point for the application
ENTRYPOINT ["dotnet", "Basic3TierAPI.dll"]
