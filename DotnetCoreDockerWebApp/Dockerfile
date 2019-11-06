FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
COPY . .
RUN dotnet restore "DotnetCoreDockerWebApp.csproj"



FROM build AS publish
RUN dotnet publish "DotnetCoreDockerWebApp.csproj" -c Release -o /app

FROM base AS final

COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DotnetCoreDockerWebApp.dll"]
