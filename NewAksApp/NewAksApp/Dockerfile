FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["NewAksApp/NewAksApp.csproj", "NewAksApp/"]
RUN dotnet restore "NewAksApp/NewAksApp.csproj"
COPY . .
WORKDIR "/src/NewAksApp"
RUN dotnet build "NewAksApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "NewAksApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NewAksApp.dll"]