FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["iInvestor.Service/iInvestor.Service.fsproj", "iInvestor.Service/"]
RUN dotnet restore "iInvestor.Service/iInvestor.Service.fsproj"
COPY . .
WORKDIR "/src/iInvestor.Service"
RUN dotnet build "iInvestor.Service.fsproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "iInvestor.Service.fsproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "iInvestor.Service.dll"]