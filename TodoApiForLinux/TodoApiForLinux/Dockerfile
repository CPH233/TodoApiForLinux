FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["TodoApiForLinux/TodoApiForLinux.csproj", "TodoApiForLinux/"]
RUN dotnet restore "TodoApiForLinux/TodoApiForLinux.csproj"
COPY . .
WORKDIR "/src/TodoApiForLinux"
RUN dotnet build "TodoApiForLinux.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TodoApiForLinux.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TodoApiForLinux.dll"]