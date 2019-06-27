FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Scheduler/Scheduler.csproj", "Scheduler/"]
RUN dotnet restore "Scheduler/Scheduler.csproj"
COPY . .
WORKDIR "/src/Scheduler"
RUN dotnet build "Scheduler.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Scheduler.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Scheduler.dll"]