FROM microsoft/dotnet:2.1-sdk
WORKDIR /app
COPY *.csproj ./
RUN dotnet restore
COPY . ./
ENTRYPOINT [ "dotnet", "run" ]