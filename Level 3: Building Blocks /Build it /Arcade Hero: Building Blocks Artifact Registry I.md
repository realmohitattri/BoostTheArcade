```
gcloud auth list

export REGION=$(gcloud compute project-info describe --format="value(commonInstanceMetadata.items[google-compute-default-region])")

gcloud services enable artifactregistry.googleapis.com

gcloud artifacts repositories create container-registry --location=$REGION --repository-format=docker

```
