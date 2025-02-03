### Code 1 [CREATE DATAPROC CLUSTER]:
```
# Prompt user for input
echo "Enter the region:"
read REGION
echo "Enter the zone:"
read ZONE
echo "Enter the project ID:"
read PROJECT_ID

# Create Dataproc cluster
gcloud dataproc clusters create qlab \
  --enable-component-gateway \
  --region $REGION \
  --zone $ZONE \
  --master-machine-type e2-standard-4 \
  --master-boot-disk-type pd-balanced \
  --master-boot-disk-size 100 \
  --num-workers 2 \
  --worker-machine-type e2-standard-2 \
  --worker-boot-disk-size 100 \
  --image-version 2.2-debian12 \
  --project $PROJECT_ID

```

---
### above code will take upto 4 minutes...

### Code 2 [SUBMIT SPARK JOB]

```
# Prompt user for input
echo "Enter the region:"
read REGION

# Submit Spark job to the cluster
gcloud dataproc jobs submit spark \
  --region $REGION \
  --cluster qlab \
  --class org.apache.spark.examples.SparkPi \
  --jars file:///usr/lib/spark/examples/jars/spark-examples.jar \
  -- 1000


```
