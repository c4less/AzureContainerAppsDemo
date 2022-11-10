FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["TasksTrackerDemo.TasksManager.Backend.Api/TasksTrackerDemo.TasksManager.Backend.Api.csproj", "TasksTrackerDemo.TasksManager.Backend.Api/"]
RUN dotnet restore "TasksTrackerDemo.TasksManager.Backend.Api/TasksTrackerDemo.TasksManager.Backend.Api.csproj"
COPY . .
WORKDIR "/src/TasksTrackerDemo.TasksManager.Backend.Api"
RUN dotnet build "TasksTrackerDemo.TasksManager.Backend.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TasksTrackerDemo.TasksManager.Backend.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TasksTrackerDemo.TasksManager.Backend.Api.dll"]
