FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app

EXPOSE 5000

ENV DATA=test
ENV ASPNETCORE_URLS=http://*:5000

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["WebApiNetDocker.csproj", "./"]
RUN dotnet restore "./WebApiNetDocker.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "WebApiNetDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApiNetDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApiNetDocker.dll"]