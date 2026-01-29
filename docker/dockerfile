# ---------- Build Stage ----------
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy csproj and restore
COPY src/SampleWebApi/SampleWebApi.csproj ./SampleWebApi/
RUN dotnet restore ./SampleWebApi/SampleWebApi.csproj

# Copy source code
COPY src/ ./src/

# Build
RUN dotnet publish src/SampleWebApi \
    -c Release \
    -o /app/publish

# ---------- Runtime Stage ----------
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

COPY --from=build /app/publish .

EXPOSE 8080
ENTRYPOINT ["dotnet", "SampleWebApi.dll"]
