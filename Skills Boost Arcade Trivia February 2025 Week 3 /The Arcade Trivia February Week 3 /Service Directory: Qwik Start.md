```
#!/bin/bash

# Define color variables
YELLOW_TEXT=$'\033[0;33m'
MAGENTA_TEXT=$'\033[0;35m'
NO_COLOR=$'\033[0m'
GREEN_TEXT=$'\033[0;32m'
RED_TEXT=$'\033[0;31m'
CYAN_TEXT=$'\033[0;36m'
BOLD_TEXT=`tput bold`
RESET_FORMAT=`tput sgr0`
BLUE_TEXT=$'\033[0;34m'

# Welcome message
echo "${BOLD_TEXT}${CYAN_TEXT}Starting the process...${RESET_FORMAT}"
echo ""

# Prompt user for LOCATION input
read -p "${BOLD_TEXT}${YELLOW_TEXT}Enter location: ${RESET_FORMAT}" LOCATION

# Validate user input
if [ -z "$LOCATION" ]; then
  echo "${BOLD_TEXT}${RED_TEXT}Error: Location cannot be empty. Please rerun the script and provide a valid location.${RESET_FORMAT}"
  exit 1
fi

echo ""
echo "${BOLD_TEXT}${GREEN_TEXT}Step 2: Enabling the Service Directory API...${RESET_FORMAT}"
gcloud services enable servicedirectory.googleapis.com

# Sleep to allow API enablement to propagate
echo "${BOLD_TEXT}${YELLOW_TEXT}Waiting 15 seconds for the API to be fully enabled...${RESET_FORMAT}"
sleep 15

echo ""
echo "${BOLD_TEXT}${GREEN_TEXT}Step 3: Creating a Service Directory namespace...${RESET_FORMAT}"
gcloud service-directory namespaces create example-namespace \
   --location $LOCATION

echo ""
echo "${BOLD_TEXT}${GREEN_TEXT}Step 4: Creating a Service Directory service...${RESET_FORMAT}"
gcloud service-directory services create example-service \
   --namespace example-namespace \
   --location $LOCATION

echo ""
echo "${BOLD_TEXT}${GREEN_TEXT}Step 5: Creating a Service Directory endpoint...${RESET_FORMAT}"
gcloud service-directory endpoints create example-endpoint \
   --address 0.0.0.0 \
   --port 80 \
   --service example-service \
   --namespace example-namespace \
   --location $LOCATION

echo ""
echo "${BOLD_TEXT}${GREEN_TEXT}Step 6: Creating a DNS Managed Zone...${RESET_FORMAT}"
gcloud dns managed-zones create example-zone-name \
   --dns-name myzone.example.com \
   --description quickgcplab \
   --visibility private \
   --networks https://www.googleapis.com/compute/v1/projects/$DEVSHELL_PROJECT_ID/global/networks/default \
   --service-directory-namespace https://servicedirectory.googleapis.com/v1/projects/$DEVSHELL_PROJECT_ID/locations/$LOCATION/namespaces/example-namespace


# Safely delete the script if it exists
SCRIPT_NAME="arcadecrew.sh"
if [ -f "$SCRIPT_NAME" ]; then
    echo -e "${BOLD_TEXT}${RED_TEXT}Deleting the script ($SCRIPT_NAME) for safety purposes...${RESET_FORMAT}${NO_COLOR}"
    rm -- "$SCRIPT_NAME"
fi

echo
echo
# Completion message
echo -e "${MAGENTA_TEXT}${BOLD_TEXT}Lab Completed Successfully!${RESET_FORMAT}"
echo -e "${GREEN_TEXT}${BOLD_TEXT}Subscribe our Channel:${RESET_FORMAT} ${BLUE_TEXT}${BOLD_TEXT}https://www.youtube.com/@BoostTheArcade ${RESET_FORMAT}"
echo
```
