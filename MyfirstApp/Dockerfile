#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["MyfirstApp/MyfirstApp.csproj", "MyfirstApp/"]
RUN dotnet restore "MyfirstApp/MyfirstApp.csproj"
COPY . .
WORKDIR "/src/MyfirstApp"
RUN dotnet build "MyfirstApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyfirstApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyfirstApp.dll"]