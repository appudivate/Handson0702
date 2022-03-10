#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["WebApplication1Docker/WebApplication1Docker.csproj", "WebApplication1Docker/"]
RUN dotnet restore "WebApplication1Docker/WebApplication1Docker.csproj"
COPY . .
WORKDIR "/src/WebApplication1Docker"
RUN dotnet build "WebApplication1Docker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication1Docker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication1Docker.dll"]