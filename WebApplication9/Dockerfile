FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["WebApplication9/WebApplication9.csproj", "WebApplication9/"]
RUN dotnet restore "WebApplication9/WebApplication9.csproj"
COPY . .
WORKDIR "/src/WebApplication9"
RUN dotnet build "WebApplication9.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApplication9.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication9.dll"]