FROM mcr.microsoft.com/dotnet/sdk:6.0 AS builder

WORKDIR /src
COPY src/web-api/web-api.csproj ./web-api/

WORKDIR /src/web-api
RUN dotnet restore

COPY src/web-api /src/web-api/
RUN dotnet publish -c Release -o /out web-api.csproj

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
ARG BUILD_CONFIGURATION=Debug
ENV ASPNETCORE_ENVIRONMENT=Development
ENV DOTNET_USE_POLLING_FILE_WATCHER=true  
ENV ASPNETCORE_URLS=http://+:80  

EXPOSE 80
ENTRYPOINT ["dotnet", "web-api.dll"]
CMD ["-m", "console", "-dp", "6"]

WORKDIR /app
COPY --from=builder /out/ .