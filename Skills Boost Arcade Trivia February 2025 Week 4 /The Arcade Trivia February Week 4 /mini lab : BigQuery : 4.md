```
export PROJECT_ID=$(gcloud config get-value project)
export REGION=$(gcloud compute project-info describe --format="value(commonInstanceMetadata.items[google-compute-default-region])")

export BUCKET_NAME=

bq load --source_format=CSV --autodetect products.products_information gs://$BUCKET_NAME/products.csv 

bq query --use_legacy_sql=false "CREATE SEARCH INDEX IF NOT EXISTS products.p_i_search_index ON products.products_information (ALL COLUMNS);"

bq query --use_legacy_sql=false "SELECT * FROM products.products_information WHERE SEARCH(STRUCT(), '22 oz Water Bottle') = TRUE;"
```
