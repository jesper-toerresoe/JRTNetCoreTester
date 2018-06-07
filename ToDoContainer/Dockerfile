FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY ToDoContainer/ToDoContainer.csproj ToDoContainer/
RUN dotnet restore ToDoContainer/ToDoContainer.csproj
COPY . .
WORKDIR /src/ToDoContainer
RUN dotnet build ToDoContainer.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ToDoContainer.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ToDoContainer.dll"]
