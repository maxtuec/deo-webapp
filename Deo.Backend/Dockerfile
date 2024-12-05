#FROM mcr.microsoft.com/dotnet/sdk:8.0-alpine3.20

#WORKDIR /root

#COPY . .

#RUN dotnet build

#EXPOSE 6680

#ENTRYPOINT ["dotnet", "run"]

FROM mcr.microsoft.com/dotnet/sdk:8.0-alpine3.20 AS build-stage
WORKDIR /build
COPY . .
RUN dotnet publish

FROM mcr.microsoft.com/dotnet/aspnet:8.0-alpine3.20
WORKDIR /app
COPY --from=build-stage /build/bin/Release/net8.0/publish .
ENV ASPNETCORE_URLS=http://*.:3000
ENTRYPOINT ["/app/Deo.Backend"]

EXPOSE 3000/tcp

# docker build -f Dockerfile -t deo-backend:latest .
# docker run -d --rm -p 3000:3000 deo-backend:latest

#from karder
# docker build -t deo-backend:latest .
# docker run --name deo-backend -d --network deo-network -p 3000:3000 deo-backend:latest --urls http://0.0.0.0:3000