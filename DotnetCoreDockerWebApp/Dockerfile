FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["DotnetCoreDockerWebApp/DotnetCoreDockerWebApp.csproj", "DotnetCoreDockerWebApp/"]
RUN dotnet restore "DotnetCoreDockerWebApp/DotnetCoreDockerWebApp.csproj"
COPY . .
WORKDIR "/src/DotnetCoreDockerWebApp"
RUN dotnet build "DotnetCoreDockerWebApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DotnetCoreDockerWebApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DotnetCoreDockerWebApp.dll"]