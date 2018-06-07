FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY ToDoAPIContainer/ToDoAPIContainer.csproj ToDoAPIContainer/
RUN dotnet restore ToDoAPIContainer/ToDoAPIContainer.csproj
COPY . .
WORKDIR /src/ToDoAPIContainer
RUN dotnet build ToDoAPIContainer.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ToDoAPIContainer.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ToDoAPIContainer.dll"]
