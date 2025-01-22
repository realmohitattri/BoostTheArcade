## Run the following Commands in Google CloudShell

    #!/bin/bash

    # Define color variables
    COLOR_RESET=$(tput sgr0)
    COLOR_BOLD=$(tput bold)
    COLOR_HEADER=$(tput setaf 4)  # Blue for headers
    COLOR_SUCCESS=$(tput setaf 2)  # Green for success messages
    COLOR_ALERT=$(tput setaf 1)  # Red for alerts
    BG_HIGHLIGHT=$(tput setab 7)  # White background for emphasis

    # Separator for readability
    SEPARATOR="----------------------------------------------------"

    # Start script execution
    echo "${BG_HIGHLIGHT}${COLOR_BOLD}${COLOR_HEADER}Starting Execution...${COLOR_RESET}"
    echo "${SEPARATOR}"

    # Run queries
    bq query --use_legacy_sql=false \
    'SELECT * FROM `billing_dataset.enterprise_billing` WHERE Cost > 0'

    bq query --use_legacy_sql=false \
    'SELECT
    project.name as Project_Name,
    service.description as Service,
    location.country as Country,
    cost as Cost
    FROM `billing_dataset.enterprise_billing`;'

    bq query --use_legacy_sql=false \
    'SELECT
    project.name as Project_Name,
    service.description as Service,
    location.country as Country,
    cost as Cost
    FROM `billing_dataset.enterprise_billing`;'

    bq query --use_legacy_sql=false \
    'SELECT project.id, count(*) as count from `billing_dataset.enterprise_billing` GROUP BY project.id'

    bq query --use_legacy_sql=false \
    'SELECT ROUND(SUM(cost),2) as Cost, project.name from `billing_dataset.enterprise_billing` GROUP BY project.name'

    # Display completion message
    echo "${SEPARATOR}"
    echo "${COLOR_BOLD}${COLOR_SUCCESS}Congratulations for completing the lab!${COLOR_RESET}"

▶ Go to BigQuery from [here](https://console.cloud.google.com/bigquery?)

    SELECT CONCAT(service.description, ' : ',sku.description) as Line_Item FROM `billing_dataset.enterprise_billing` GROUP BY 1


    SELECT CONCAT(service.description, ' : ',sku.description) as Line_Item, Count(*) as NUM FROM `billing_dataset.enterprise_billing` GROUP BY CONCAT(service.description, ' : ',sku.description)
