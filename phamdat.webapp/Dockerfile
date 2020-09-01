#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["phamdat.webapp/phamdat.webapp.csproj", "phamdat.webapp/"]
RUN dotnet restore "phamdat.webapp/phamdat.webapp.csproj"
COPY . .
WORKDIR "/src/phamdat.webapp"
RUN dotnet build "phamdat.webapp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "phamdat.webapp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "phamdat.webapp.dll"]