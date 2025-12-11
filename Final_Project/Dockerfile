# Base image with the ASP.NET Core runtime
FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS base
WORKDIR /app

# Render expects services to listen on port 10000
EXPOSE 10000
ENV ASPNETCORE_URLS=http://+:10000

# Build image with the .NET SDK
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src

# COPY the project file and restore deps
COPY ["Final_Project.csproj", "./"]
RUN dotnet restore "Final_Project.csproj"

# Copy everything else and publish
COPY . .
RUN dotnet publish "Final_Project.csproj" -c Release -o /app/publish

# Final image
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Final_Project.dll"]