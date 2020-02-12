FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["AccountInfoService/AccountInfoService.csproj", "AccountInfoService/"]
RUN dotnet restore "AccountInfoService/AccountInfoService.csproj"

COPY . .
WORKDIR "/src/AccountInfoService"
RUN dotnet build "AccountInfoService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AccountInfoService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AccountInfoService.dll"]