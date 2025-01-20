## Monitoring Multiple Projects with Cloud Monitoring | GSP090

# Run the following Commands in CloudShell
    export PROJECT_2=
    export ZONE=


# Then Paste below code    

    #!/bin/bash
    # Define color variables
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
    echo "${BG_MAGENTA}${BOLD}Starting Execution${RESET}"
    gcloud config set project $PROJECT_2
    gcloud compute instances create instance2 \
    --zone=$ZONE \
    --machine-type=e2-medium
    echo "${YELLOW}${BOLD}NOW${RESET}" "${WHITE}${BOLD}FOLLOW${RESET}" "${GREEN}${BOLD}VIDEO'S INSTRUCTIONS${RESET}"

#-----------------------------------------------------end----------------------------------------------------------#
    

※ Go to `Create group` from here: [Group](https://console.cloud.google.com/monitoring/groups?pli=1)
※ Name your group `DemoGroup`
※ In the third field (Value), type in `instance`
※ For Uptime check Title: enter `DemoGroup uptime check`

     #!/bin/bash
     # Define color variables
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
     echo "${BG_MAGENTA}${BOLD}Starting Execution${RESET}"
     cat > awesome.json <<EOF_END
     {
     "displayName": "Uptime Check Policy",
     "userLabels": {},
     "conditions": [
     {
      "displayName": "VM Instance - Check passed",
      "conditionAbsent": {
        "filter": "resource.type = \"gce_instance\" AND metric.type = \"monitoring.googleapis.com/uptime_check/check_passed\" AND metric.labels.check_id = \"demogroup-uptime-check-f-UeocjSHdQ\"",
        "aggregations": [
          {
            "alignmentPeriod": "300s",
            "crossSeriesReducer": "REDUCE_NONE",
            "perSeriesAligner": "ALIGN_FRACTION_TRUE"
          }
        ],
        "duration": "300s",
        "trigger": {
          "count": 1
        }
      }
    }
    ],
    "alertStrategy": {},
    "combiner": "OR",
    "enabled": true,
    "notificationChannels": [],
    "severity": "SEVERITY_UNSPECIFIED"
    }
    EOF_END
    gcloud alpha monitoring policies create --policy-from-file="awesome.json"
    echo "${BG_RED}${BOLD}Congratulations For Completing The Lab !!! Subscribe Boost The Arcade${RESET}"

[Boost The Arcade](https://www.youtube.com/@BoostTheArcade)
