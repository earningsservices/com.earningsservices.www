#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["com.earningsservices.www/com.earningsservices.www.csproj", "com.earningsservices.www/"]
RUN dotnet restore "com.earningsservices.www/com.earningsservices.www.csproj"
COPY . .
WORKDIR "/src/com.earningsservices.www"
RUN dotnet build "com.earningsservices.www.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "com.earningsservices.www.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "com.earningsservices.www.dll"]