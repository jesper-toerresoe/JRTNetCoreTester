FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ToDoContainerLinux/ToDoContainerLinux.csproj ToDoContainerLinux/
RUN dotnet restore ToDoContainerLinux/ToDoContainerLinux.csproj
COPY . .
WORKDIR /src/ToDoContainerLinux
RUN dotnet build ToDoContainerLinux.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ToDoContainerLinux.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ToDoContainerLinux.dll"]
