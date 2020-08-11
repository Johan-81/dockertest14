#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["dockertest14/dockertest14.csproj", "dockertest14/"]
RUN dotnet restore "dockertest14/dockertest14.csproj"
COPY . .
WORKDIR "/src/dockertest14"
RUN dotnet build "dockertest14.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dockertest14.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dockertest14.dll"]