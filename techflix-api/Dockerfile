FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /source

# copy csproj and restore as distinct layers
COPY *.sln .
COPY TechFlixApi/*.csproj ./TechFlixApi/
COPY TechFlixApi.Tests/*.csproj ./TechFlixApi.Tests/
# RUN dotnet restore

# copy everything else and build app
COPY TechFlixApi/. ./TechFlixApi/
WORKDIR /source/TechFlixApi/
RUN dotnet restore
RUN dotnet publish -c release -o /app --no-restore

# final stage/image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["dotnet", "TechFlixApi.dll"]