FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 24870
EXPOSE 44364

FROM microsoft/dotnet:2.1-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY WebApplication5/WebApplication5.csproj WebApplication5/
RUN dotnet restore WebApplication5/WebApplication5.csproj
COPY . .
WORKDIR /src/WebApplication5
RUN dotnet build WebApplication5.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WebApplication5.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication5.dll"]
