# Base runtime image (Linux)
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# SDK image for build (Linux)
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY . .
RUN dotnet restore "PracticalWork3/PracticalWork3/PracticalWork3.csproj"
RUN dotnet build "PracticalWork3/PracticalWork3/PracticalWork3.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PracticalWork3/PracticalWork3/PracticalWork3.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PracticalWork3.dll"]
