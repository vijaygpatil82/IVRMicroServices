FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["StartInteractionService/StartInteractionService.csproj", "StartInteractionService/"]
RUN dotnet restore "StartInteractionService/StartInteractionService.csproj"

COPY . .
WORKDIR "/src/StartInteractionService"
RUN dotnet build "StartInteractionService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "StartInteractionService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "StartInteractionService.dll"]