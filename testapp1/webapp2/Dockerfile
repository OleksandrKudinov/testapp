#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["webapp2/webapp2.csproj", "webapp2/"]
RUN dotnet restore "webapp2/webapp2.csproj"
COPY . .
WORKDIR "/src/webapp2"
RUN dotnet build "webapp2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "webapp2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "webapp2.dll"]