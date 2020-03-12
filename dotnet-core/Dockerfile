FROM microsoft/dotnet:sdk AS build-env
WORKDIR /app

RUN mkdir /output
COPY . ./

WORKDIR /app/Builders.eCommerce.WebApi
RUN ls -la
RUN dotnet publish --configuration Release --verbosity d -o /output

FROM microsoft/dotnet:aspnetcore-runtime
ENV ASPNETCORE_URLS http://*:8080

WORKDIR /app
COPY --from=build-env /output .
EXPOSE 8080

ENTRYPOINT ["dotnet", "Builders.eCommerce.WebApi.dll"]