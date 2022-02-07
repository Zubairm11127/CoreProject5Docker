#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["CoreProject5/CoreProject5.csproj", "CoreProject5/"]
RUN dotnet restore "CoreProject5/CoreProject5.csproj"
COPY . .
WORKDIR "/src/CoreProject5"
RUN dotnet build "CoreProject5.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CoreProject5.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CoreProject5.dll"]