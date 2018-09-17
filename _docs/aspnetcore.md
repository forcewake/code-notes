---
title: ASP.NET Core
category: .NET Core
order: 1
---

## Deploy ASP.NET Core to Azure Container Registry

``` bash
docker login mycr.azurecr.io -u jwendl -p P@SSW0rd!
dotnet publish -c Release -o out
cp Dockerfile out
docker build -t music-store:v1 out
docker run -d -p 8080:8080 music-store:v1
docker ps -a
docker tag 8b mycr.azurecr.io/folder/image-name
docker push mycr.azurecr.io/folder/image-name
```
