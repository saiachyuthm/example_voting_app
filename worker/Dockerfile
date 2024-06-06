FROM --platform=linux/amd64/v3 mcr.microsoft.com/dotnet/sdk:7.0 as build

ARG TARGETPLATFORM=linux
ARG TARGETARCH=linux-x64
ARG BUILDPLATFORM=linux/amd64/v3

RUN echo "I am running on ${BUILDPLATFORM}, building for ${TARGETPLATFORM}"

WORKDIR /source
COPY *.csproj .
RUN dotnet restore -r ${TARGETARCH}

COPY . .
RUN dotnet publish -c release -o /app -r ${TARGETARCH} --self-contained false --no-restore

FROM mcr.microsoft.com/dotnet/runtime:7.0
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "Worker.dll"]

