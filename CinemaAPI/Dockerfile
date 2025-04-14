# Usar una imagen base de .NET
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

# Usar la imagen SDK de .NET para compilar el proyecto
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["cinemaapi/cinemaapi.csproj", "cinemaapi/"]
RUN dotnet restore "cinemaapi/cinemaapi.csproj"
COPY . .
WORKDIR "/src/cinemaapi"
RUN dotnet build "cinemaapi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "cinemaapi.csproj" -c Release -o /app/publish

# Configuración final para el contenedor
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "cinemaapi.dll"]
