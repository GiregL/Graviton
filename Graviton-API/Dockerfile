FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Graviton-API/Graviton-API.csproj", "Graviton-API/"]
RUN dotnet restore "Graviton-API/Graviton-API.csproj"
COPY . .
WORKDIR "/src/Graviton-API"
RUN dotnet build "Graviton-API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Graviton-API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Graviton-API.dll"]
