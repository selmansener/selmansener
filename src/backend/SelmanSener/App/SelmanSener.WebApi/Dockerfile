#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["App/SelmanSener.WebApi/SelmanSener.WebApi.csproj", "App/SelmanSener.WebApi/"]
RUN dotnet restore "App/SelmanSener.WebApi/SelmanSener.WebApi.csproj"
COPY . .
WORKDIR "/src/App/SelmanSener.WebApi"
RUN dotnet build "SelmanSener.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SelmanSener.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SelmanSener.WebApi.dll"]