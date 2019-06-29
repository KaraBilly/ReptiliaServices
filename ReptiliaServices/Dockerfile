FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["ReptiliaServices/ReptiliaServices.csproj", "ReptiliaServices/"]
RUN dotnet restore "ReptiliaServices/ReptiliaServices.csproj"
COPY . .
WORKDIR "/src/ReptiliaServices"
RUN dotnet build "ReptiliaServices.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ReptiliaServices.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ReptiliaServices.dll"]