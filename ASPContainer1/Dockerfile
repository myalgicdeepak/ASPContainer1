FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ASPContainer1/ASPContainer1.csproj ASPContainer1/
RUN dotnet restore ASPContainer1/ASPContainer1.csproj
COPY . .
WORKDIR /src/ASPContainer1
RUN dotnet build ASPContainer1.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ASPContainer1.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ASPContainer1.dll"]
