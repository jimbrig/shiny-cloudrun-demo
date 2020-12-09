# Running Shiny app on Google Cloud Run

![Build and Deploy to Cloud Run](https://github.com/jimbrig/shiny-cloudrun-demo/workflows/Build%20and%20Deploy%20to%20Cloud%20Run/badge.svg)

```
PROJECTID=$(gcloud config get-value project)
```

```
docker build . -t gcr.io/$PROJECTID/shinyrun
```

Test locally
```
docker run --rm -p 8080:8080 gcr.io/$PROJECTID/shinyrun:latest
```

Push image to Google Registry
```
gcloud auth configure-docker
docker push gcr.io/$PROJECTID/shinyrun
```

Alternatively, ultilize Googld Builds to build image
```
gcloud builds submit --tag gcr.io/$PROJECTID/shinyrun
```

Deploy to Google Cloud Run
```
gcloud run deploy --image gcr.io/$PROJECTID/shinyrun --platform managed --max-instances 1
```
