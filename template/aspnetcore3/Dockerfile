FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["Server.csproj", ""]
RUN dotnet restore "./Server.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "Server.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Server.csproj" -c Release -o /app/publish

FROM openfaas/of-watchdog:0.7.2 as watchdog

FROM base AS final

COPY --from=watchdog /fwatchdog /usr/bin/fwatchdog
RUN chmod +x /usr/bin/fwatchdog

WORKDIR /app
COPY --from=publish /app/publish .


ENV fprocess="dotnet ./Server.dll"
ENV cgi_headers="true"
ENV mode="http"
ENV upstream_url="http://127.0.0.1"

EXPOSE 8080
CMD ["fwatchdog"]