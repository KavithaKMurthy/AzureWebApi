FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ./DockerExample.csproj DockerExample/
RUN dotnet restore ./DockerExample/DockerExample.csproj

COPY . DockerExample/
RUN dotnet build ./DockerExample/DockerExample.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ./DockerExample/DockerExample.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerExample.dll"]
