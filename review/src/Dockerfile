FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /app
COPY Review.Web/Review.Web.csproj ./Review.Web/
RUN dotnet restore Review.Web/Review.Web.csproj
COPY . .
WORKDIR /app/Review.Web
RUN dotnet build Review.Web.csproj -c Release -o /app/build
FROM build AS publish
RUN dotnet publish Review.Web.csproj -c Release -o /app/publish
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Review.Web.dll"]
