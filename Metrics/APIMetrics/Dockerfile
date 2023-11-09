FROM mcr.microsoft.com/dotnet/sdk:7.0.403 AS build-env
WORKDIR /app

# Copiar csproj e restaurar dependencias
COPY *.csproj ./
RUN dotnet restore

# Build da aplicacao
COPY . ./
RUN dotnet publish -c Release -o out

# Build da imagem
FROM mcr.microsoft.com/dotnet/aspnet:7.0.13
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "APIMetrics.dll"]