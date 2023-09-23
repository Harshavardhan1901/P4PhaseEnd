#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["P4PhaseEndProject/P4PhaseEndProject.csproj", "P4PhaseEndProject/"]
RUN dotnet restore "P4PhaseEndProject/P4PhaseEndProject.csproj"
COPY . .
WORKDIR "/src/P4PhaseEndProject"
RUN dotnet build "P4PhaseEndProject.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "P4PhaseEndProject.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "P4PhaseEndProject.dll"]