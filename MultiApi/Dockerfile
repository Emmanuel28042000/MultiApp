#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["MultiApi/MultiApi.csproj", "MultiApi/"]
RUN dotnet restore "MultiApi/MultiApi.csproj"
COPY . .
WORKDIR "/src/MultiApi"
RUN dotnet build "MultiApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MultiApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MultiApi.dll"]
