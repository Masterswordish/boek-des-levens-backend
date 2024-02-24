FROM mcr.microsoft.com/dotnet/runtime:8.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Boek-Des-Levens-Backend/Boek-Des-Levens-Backend.csproj", "Boek-Des-Levens-Backend/"]
RUN dotnet restore "Boek-Des-Levens-Backend/Boek-Des-Levens-Backend.csproj"
COPY . .
WORKDIR "/src/Boek-Des-Levens-Backend"
RUN dotnet build "Boek-Des-Levens-Backend.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Boek-Des-Levens-Backend.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Boek-Des-Levens-Backend.dll"]
