### - KANIKO COM DOCKER
```
cd dotnet-core-api-prod

docker run -v ~/builders/inovacao.json:/kaniko/config.json \
  -e GOOGLE_APPLICATION_CREDENTIALS="/kaniko/config.json" \
  -v $(pwd):/app gcr.io/kaniko-project/executor:latest \
  --dockerfile=/Builders.eCommerce.WebApi/Dockerfile \
  --context=/app \
  --destination=gcr.io/$(gcloud config --quiet get-value project)/meetup-dotnetcore-app:v2.0.1
```