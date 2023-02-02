FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ConsoleApp-docker/ConsoleApp-docker.csproj", "ConsoleApp-docker/"]
RUN dotnet restore "ConsoleApp-docker/ConsoleApp-docker.csproj"
COPY . .
WORKDIR "/src/ConsoleApp-docker"
RUN dotnet build "ConsoleApp-docker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ConsoleApp-docker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConsoleApp-docker.dll"]
