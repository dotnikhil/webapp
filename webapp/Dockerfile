FROM mcr.microsoft.com/dotnet/aspnet:8.0 as base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:8.0 as build
WORKDIR /src

COPY webapp.csproj .
RUN dotnet restore webapp.csproj

COPY . .
RUN dotnet build webapp.csproj -o ./build

FROM build as publish
RUN dotnet publish webapp.csproj -c Release -o ./publish /p:UseAppHost=false

FROM base as final
ENV ASPNETCORE_URLS=http://*:8081
COPY --from=publish /src/publish .
ENTRYPOINT ["dotnet", "webapp.dll"]