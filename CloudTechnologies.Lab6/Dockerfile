FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS base
USER $APP_UID
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["CloudTechnologies.Lab6/CloudTechnologies.Lab6.csproj", "CloudTechnologies.Lab6/"]
RUN dotnet restore "CloudTechnologies.Lab6/CloudTechnologies.Lab6.csproj"
COPY . .
WORKDIR "/src/CloudTechnologies.Lab6"
RUN dotnet build "./CloudTechnologies.Lab6.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./CloudTechnologies.Lab6.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CloudTechnologies.Lab6.dll"]
