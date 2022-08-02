FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["ContainedWebApi/ContainedWebApi.csproj", "ContainedWebApi/"]

RUN dotnet restore "ContainedWebApi/ContainedWebApi.csproj"
COPY . .
WORKDIR "/src/ContainedWebApi"
RUN dotnet build "ContainedWebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ContainedWebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ContainedWebApi.dll"]