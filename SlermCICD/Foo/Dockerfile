#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app
EXPOSE 80
EXPOSE 443

COPY ["Foo.csproj", "./"]
RUN dotnet restore "Foo.csproj"

COPY . .

RUN dotnet build "Foo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Foo.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Foo.dll"]