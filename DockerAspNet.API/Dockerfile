FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 5189

ENV ASPNETCORE_URLS=http://+:5189;
ENV ASPNETCORE_ENVIRONMENT=Development

USER app
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG configuration=Release
WORKDIR /src
COPY ["DockerAspNet.API.csproj", "./"]
RUN dotnet restore "DockerAspNet.API.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "DockerAspNet.API.csproj" -c $configuration -o /app/build

FROM build AS publish
ARG configuration=Release
RUN dotnet publish "DockerAspNet.API.csproj" -c $configuration -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerAspNet.API.dll"]
