FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["DockerTest_Linux/DockerTest_Linux.csproj", "DockerTest_Linux/"]
RUN dotnet restore "DockerTest_Linux/DockerTest_Linux.csproj"
COPY . .
WORKDIR "/src/DockerTest_Linux"
RUN dotnet build "DockerTest_Linux.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DockerTest_Linux.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerTest_Linux.dll"]