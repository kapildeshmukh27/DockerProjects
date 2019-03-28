FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY MyFirstDockerApp/MyFirstDockerApp.csproj MyFirstDockerApp/
RUN dotnet restore MyFirstDockerApp/MyFirstDockerApp.csproj
COPY . .
WORKDIR /src/MyFirstDockerApp
RUN dotnet build MyFirstDockerApp.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish MyFirstDockerApp.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MyFirstDockerApp.dll"]
