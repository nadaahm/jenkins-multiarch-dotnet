# jenkins-multiarch-dotnet

```bash
docker build -t ahmednada/web-app-multiarch:manifest-amd64 --build-arg ARCH=amd64/ -f Dockerfile.x64 .
```

```bash
docker build -t ahmednada/web-app-multiarch:manifest-arm64v8 --build-arg ARCH=arm64v8/ -f Dockerfile.arm64 .
```

```bash
 docker run --rm -d -p 8080:80 --name myapp ahmednada/web-app-multiarch:manifest-arm64v8
 ```
