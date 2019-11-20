FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["Podu.NetCoreWeb/Podu.NetCoreWeb.csproj", "Podu.NetCoreWeb/"]
RUN dotnet restore "Podu.NetCoreWeb/Podu.NetCoreWeb.csproj"
COPY . .
WORKDIR "/src/Podu.NetCoreWeb"
RUN dotnet build "Podu.NetCoreWeb.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Podu.NetCoreWeb.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Podu.NetCoreWeb.dll"]