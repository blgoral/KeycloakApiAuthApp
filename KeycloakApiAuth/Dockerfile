FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["KeycloakApiAuth/KeycloakApiAuth.csproj", "KeycloakApiAuth/"]
RUN dotnet restore "KeycloakApiAuth/KeycloakApiAuth.csproj"
COPY . .
WORKDIR "/src/KeycloakApiAuth"
RUN dotnet build "KeycloakApiAuth.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "KeycloakApiAuth.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "KeycloakApiAuth.dll"]
