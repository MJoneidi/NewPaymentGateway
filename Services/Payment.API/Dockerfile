#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 8001/tcp
ENV ASPNETCORE_URLS=http://+:8001

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Services/Payment.API/Payment.API.csproj", "Services/Payment.API/"]
COPY ["Services/Payment.Infrastructure/Payment.Infrastructure.csproj", "Services/Payment.Infrastructure/"]
COPY ["Services/Payment.Application/Payment.Application.csproj", "Services/Payment.Application/"]
COPY ["Services/Payment.Domain/Payment.Domain.csproj", "Services/Payment.Domain/"]
RUN dotnet restore "Services/Payment.API/Payment.API.csproj"
COPY . .
WORKDIR "/src/Services/Payment.API"
RUN dotnet build "Payment.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Payment.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Payment.API.dll"]
