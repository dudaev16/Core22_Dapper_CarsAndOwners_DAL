FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Core22_DapperPlus/Core22_DapperPlus.csproj", "Core22_DapperPlus/"]
RUN dotnet restore "Core22_DapperPlus/Core22_DapperPlus.csproj"
COPY . .
WORKDIR "/src/Core22_DapperPlus"
RUN dotnet build "Core22_DapperPlus.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Core22_DapperPlus.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Core22_DapperPlus.dll"]