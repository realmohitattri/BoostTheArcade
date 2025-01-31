### Run the following Commands in CloudShell

```
BLACK=`tput setaf 0`
RED=`tput setaf 1`
GREEN=`tput setaf 2`
YELLOW=`tput setaf 3`
BLUE=`tput setaf 4`
MAGENTA=`tput setaf 5`
CYAN=`tput setaf 6`
WHITE=`tput setaf 7`

BG_BLACK=`tput setab 0`
BG_RED=`tput setab 1`
BG_GREEN=`tput setab 2`
BG_YELLOW=`tput setab 3`
BG_BLUE=`tput setab 4`
BG_MAGENTA=`tput setab 5`
BG_CYAN=`tput setab 6`
BG_WHITE=`tput setab 7`

BOLD=`tput bold`
RESET=`tput sgr0`
#----------------------------------------------------start--------------------------------------------------#

echo "${YELLOW}${BOLD}Starting${RESET}" "${GREEN}${BOLD}Execution${RESET}"

gcloud pubsub topics create projects/$DEVSHELL_PROJECT_ID/topics/export-findings-pubsub-topic
gcloud pubsub subscriptions create export-findings-pubsub-topic-sub --topic=projects/$DEVSHELL_PROJECT_ID/topics/export-findings-pubsub-topic
```

* Go to `Export to Pub/Sub` from [here](https://console.cloud.google.com/security/command-center/config/continuous-exports/pubsub)

* For the continuous export name, enter in `export-findings-pubsub`.

### Run again the following Commands in CloudShell

```
export ZONE=
```

```
BLACK=`tput setaf 0`
RED=`tput setaf 1`
GREEN=`tput setaf 2`
YELLOW=`tput setaf 3`
BLUE=`tput setaf 4`
MAGENTA=`tput setaf 5`
CYAN=`tput setaf 6`
WHITE=`tput setaf 7`

BG_BLACK=`tput setab 0`
BG_RED=`tput setab 1`
BG_GREEN=`tput setab 2`
BG_YELLOW=`tput setab 3`
BG_BLUE=`tput setab 4`
BG_MAGENTA=`tput setab 5`
BG_CYAN=`tput setab 6`
BG_WHITE=`tput setab 7`

BOLD=`tput bold`
RESET=`tput sgr0`
#----------------------------------------------------start--------------------------------------------------#

echo "${YELLOW}${BOLD}Starting${RESET}" "${GREEN}${BOLD}Execution${RESET}"

export REGION="${ZONE%-*}"

PROJECT_ID=$(gcloud config get project)

gcloud compute instances create instance-1 --zone=$ZONE \
--machine-type e2-micro \
--scopes=https://www.googleapis.com/auth/cloud-platform

bq --location=$REGION --apilog=/dev/null mk --dataset \
$PROJECT_ID:continuous_export_dataset

gcloud services enable securitycenter.googleapis.com

gcloud scc bqexports create scc-bq-cont-export --dataset=projects/$PROJECT_ID/datasets/continuous_export_dataset --project=$PROJECT_ID

for i in {0..2}; do
gcloud iam service-accounts create sccp-test-sa-$i;
gcloud iam service-accounts keys create /tmp/sa-key-$i.json \
--iam-account=sccp-test-sa-$i@$PROJECT_ID.iam.gserviceaccount.com;
done
```
```
bq query --apilog=/dev/null --use_legacy_sql=false  \
"SELECT finding_id,event_time,finding.category FROM continuous_export_dataset.findings"
```

#### Note: It may take `10+ minutes` for these findings to be generated. Rerun the above command if you don't receive a similar output.

* NOW FOLLOW [VIDEO'S] INSTRUCTIONS

* Got to `Create a bucket` from [here](https://console.cloud.google.com/storage/create-bucket)

* for BUCKET NAME type `scc-export-bucket-`YOUR_PROJECT_ID

* Now go to `Export findings to Cloud Storage` from [here](https://console.cloud.google.com/security/command-center/export)

* Set the filename to `findings.jsonl`

* Go to `BigQuery Studio` from [here](https://console.cloud.google.com/bigquery)

* Set the TABLE NAME to `old_findings`

* Now paste in the following schema

```
[   
  {
    "mode": "NULLABLE",
    "name": "resource",
    "type": "JSON"
  },   
  {
    "mode": "NULLABLE",
    "name": "finding",
    "type": "JSON"
  }
]
```
