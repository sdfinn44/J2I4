#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["J2I4/J2I4.csproj", "J2I4/"]
RUN dotnet restore "J2I4/J2I4.csproj"
COPY . .
WORKDIR "/src/J2I4"
RUN dotnet build "J2I4.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "J2I4.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "J2I4.dll"]