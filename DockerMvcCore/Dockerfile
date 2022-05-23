#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["DockerMvcCore/DockerMvcCore.csproj", "DockerMvcCore/"]
RUN dotnet restore "DockerMvcCore/DockerMvcCore.csproj"
COPY . .
WORKDIR "/src/DockerMvcCore"
RUN dotnet build "DockerMvcCore.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerMvcCore.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerMvcCore.dll"]