#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 8000
ENV ASPNETCORE_URLS=http://+:8000

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Gateways/Payment.Gateway/Payment.Gateway.csproj", "Gateways/Payment.Gateway/"]
RUN dotnet restore "Gateways/Payment.Gateway/Payment.Gateway.csproj"
COPY . .
WORKDIR "/src/Gateways/Payment.Gateway"
RUN dotnet build "Payment.Gateway.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Payment.Gateway.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Payment.Gateway.dll"]