#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0-bullseye-slim AS base
RUN apt-get update && \
    apt-get install -y libc6 -f -o APT::Immediate-Configure=0 && \
    apt-get install -y \
        libicu-dev \
        libharfbuzz0b \
        libfontconfig1 \
        libfreetype6

WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM node:18-bullseye as frontend
WORKDIR /modules
COPY ["package.json", "./"]
RUN npm install

FROM mcr.microsoft.com/dotnet/sdk:7.0-bullseye-slim AS build
WORKDIR /src
RUN --mount=type=secret,id=dxnuget dotnet nuget add source $(cat /run/secrets/dxnuget) -n devexpress-nuget
COPY ["ReportingWebApp.csproj", "ReportingWebApp/"]
RUN dotnet restore "ReportingWebApp/ReportingWebApp.csproj"
COPY ["./", "ReportingWebApp/"]
WORKDIR "/src/ReportingWebApp"
COPY --from=frontend ./modules .
RUN dotnet build "ReportingWebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ReportingWebApp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ReportingWebApp.dll"]