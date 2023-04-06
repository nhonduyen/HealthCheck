#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Admin.API/Admin.API.csproj", "Admin.API/"]
RUN dotnet restore "Admin.API/Admin.API.csproj"
COPY . .
WORKDIR "/src/Admin.API"
RUN dotnet build "Admin.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Admin.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Admin.API.dll"]