#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["To_do/To_do.csproj", "To_do/"]
RUN dotnet restore "To_do/To_do.csproj"
COPY . .
WORKDIR "/src/To_do"
RUN dotnet build "To_do.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "To_do.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "To_do.dll"]

CMD ASPNETCORE_URLS=http://*:$PORT dotnet To_do.dll