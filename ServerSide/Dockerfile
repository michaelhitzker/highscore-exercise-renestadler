#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:latest AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["./ServerSide.csproj", "ServerSide/"]
RUN dotnet restore "ServerSide/ServerSide.csproj"
COPY . "ServerSide"
WORKDIR "/src/ServerSide"
RUN dotnet build "ServerSide.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ServerSide.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ServerSide.dll"]