FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-disco AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-disco AS build
WORKDIR /src
COPY ["blazor.Server/blazor.Server.csproj", "blazor.Server/"]
COPY ["blazor.Client/blazor.Client.csproj", "blazor.Client/"]
COPY ["blazor.Shared/blazor.Shared.csproj", "blazor.Shared/"]
RUN dotnet restore "blazor.Server/blazor.Server.csproj"
COPY . .
WORKDIR "/src/blazor.Server"
RUN dotnet build "blazor.Server.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "blazor.Server.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "blazor.Server.dll"]