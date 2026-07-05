# Base image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 8080

# Build image
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

COPY ["StudentApi.csproj", "./"]
RUN dotnet restore "StudentApi.csproj"

COPY . .
RUN dotnet publish "StudentApi.csproj" -c Release -o /app/publish

# Final image
FROM base AS final
WORKDIR /app

COPY --from=build /app/publish .

ENTRYPOINT ["dotnet","StudentApi.dll"]