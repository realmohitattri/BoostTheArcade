```
gcloud auth list

export REGION=$(gcloud compute project-info describe --format="value(commonInstanceMetadata.items[google-compute-default-region])")

export BUCKET_NAME=${DEVSHELL_PROJECT_ID}-bucket

gsutil mb -l $REGION gs://$BUCKET_NAME/
```
