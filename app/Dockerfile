FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
ENV ASPNETCORE_URLS=http://0.0.0.0:80
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY . . 
RUN dotnet restore
RUN dotnet build "HelloWorld.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HelloWorld.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .

ENTRYPOINT ["dotnet", "HelloWorld.dll"]

