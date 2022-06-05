FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["lab2_MVC/lab2_MVC.csproj", "lab2_MVC/"]
RUN dotnet restore "lab2_MVC/lab2_MVC.csproj"
COPY . .
WORKDIR "/src/lab2_MVC"
RUN dotnet build "lab2_MVC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "lab2_MVC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "lab2_MVC.dll"]
