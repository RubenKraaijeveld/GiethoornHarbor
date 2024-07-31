FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env
WORKDIR /app

# Copy necessary files and restore as distinct layer
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
# Build the project
RUN dotnet build -c Release --no-restore

# Publish the project
RUN dotnet publish -c Release -o /app/out --no-restore

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
COPY --from=build-env /app/out .

# Start
ENTRYPOINT ["dotnet", "AuditlogService.dll"]
