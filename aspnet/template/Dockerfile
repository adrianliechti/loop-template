FROM mcr.microsoft.com/dotnet/sdk:8.0 AS builder

WORKDIR /src

COPY *.csproj .
RUN dotnet restore

COPY . .
RUN dotnet publish -c Release -o /app --nologo --no-restore --no-self-contained


FROM mcr.microsoft.com/dotnet/aspnet:8.0

WORKDIR /app

COPY --from=builder --chown=app:app /app /app

ENV ASPNETCORE_URLS=http://+:8080
CMD ["dotnet", "/app/${APP_NAME}.dll"]