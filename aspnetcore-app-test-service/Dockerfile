FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["aspnetcore-app-test-service/aspnetcore-app-test-service.csproj", "aspnetcore-app-test-service/"]
RUN dotnet restore "aspnetcore-app-test-service/aspnetcore-app-test-service.csproj"
COPY . .
WORKDIR "/src/aspnetcore-app-test-service"
RUN dotnet build "aspnetcore-app-test-service.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "aspnetcore-app-test-service.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "aspnetcore-app-test-service.dll"]