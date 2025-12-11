# Runtime image
FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS base
WORKDIR /app

# Render wants apps to listen on port 10000
EXPOSE 10000
ENV ASPNETCORE_URLS=http://+:10000

# Build image
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src

# Copy project file and restore
COPY ["Final_Project.csproj", "./"]
RUN dotnet restore "Final_Project.csproj"

# Copy the rest of the source and publish
COPY . .
RUN dotnet publish "Final_Project.csproj" -c Release -o /app/publish

# Final image
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Final_Project.dll"]