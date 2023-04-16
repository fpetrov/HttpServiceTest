FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["HttpServiceTest/HttpServiceTest.csproj", "HttpServiceTest/"]
RUN dotnet restore "HttpServiceTest/HttpServiceTest.csproj"
COPY . .
WORKDIR "/src/HttpServiceTest"
RUN dotnet build "HttpServiceTest.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HttpServiceTest.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HttpServiceTest.dll"]
