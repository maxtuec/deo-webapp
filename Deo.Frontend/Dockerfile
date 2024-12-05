FROM mcr.microsoft.com/dotnet/sdk:8.0-alpine3.20 AS build-stage
WORKDIR /build
COPY . .
RUN dotnet publish

FROM mcr.microsoft.com/dotnet/aspnet:8.0-alpine3.20
WORKDIR /app
COPY --from=build-stage /build/bin/Release/net8.0/publish .
ENV ASPNETCORE_URLS=http://*.:2000
#ENV DEO_BACKEND_URL=http://deo-backend:3000
ENTRYPOINT ["/app/Deo.Frontend"]

EXPOSE 2000/tcp

#docker run -d --name deo-frontend -net deo-network -p 2000:2000 -e DEO_BACKEND_URL=http://deo-backend:3000 deo-frontend
#docker run -d --name deo-backend --net deo-network deo-backend

# docker build -f Dockerfile -t deo-frontend:latest .
# docker run -d --rm -p 3000:3000 deo-frontend:latest

#from karder
# docker build -t deo-frontend:latest .
# docker run --name deo-frontend -d --network deo-network -p 4000:4000 -e DEO_BACKEND_URL=http://deo-backend:3000 deo-frontend:latest --urls http://0.0.0.0:4000

