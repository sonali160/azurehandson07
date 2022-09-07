#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["azurehandson07/azurehandson07.csproj", "azurehandson07/"]
RUN dotnet restore "azurehandson07/azurehandson07.csproj"
COPY . .
WORKDIR "/src/azurehandson07"
RUN dotnet build "azurehandson07.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "azurehandson07.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "azurehandson07.dll"]