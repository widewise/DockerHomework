FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 8000

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["DockerHomework.csproj", "DockerHomework/"]
RUN dotnet restore "DockerHomework/DockerHomework.csproj"
WORKDIR "src/DockerHomework"
COPY . .
RUN dotnet build "DockerHomework.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerHomework.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerHomework.dll"]
