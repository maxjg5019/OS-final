#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["OS-fin/OS-fin.csproj", "OS-fin/"]
RUN dotnet restore "OS-fin/OS-fin.csproj"
COPY . .
WORKDIR "/src/OS-fin"
RUN dotnet build "OS-fin.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "OS-fin.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OS-fin.dll"]