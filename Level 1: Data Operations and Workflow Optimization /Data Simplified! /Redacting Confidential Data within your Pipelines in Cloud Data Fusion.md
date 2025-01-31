# Follow us on 
- <img width="25" alt="image" src="https://github.com/user-attachments/assets/0ebd7e7d-6f9b-41e9-a241-8483dca9f3f1"> [Telegram Channel](https://t.me/boostthearcade)
- <img width="25" alt="image" src="https://github.com/user-attachments/assets/dc326965-d4fa-4f1b-87f1-dbad6e3a7259"> [Boost The Arcade](https://www.youtube.com/@boostthearcade)
- <img width="26" alt="image" src="https://github.com/user-attachments/assets/d9070a07-7fce-47c5-8626-7ea98ccc46e3"> [WhatsApp](https://whatsapp.com/channel/0029Vay0oIFBqbr0rYraWJ3h)

```
export BUCKET=$GOOGLE_CLOUD_PROJECT
gcloud storage buckets create gs://$BUCKET

SERVICE_ACCOUNT=$(gcloud iam service-accounts list --filter="email~'-compute@developer.gserviceaccount.com'" --format="value(email)")
echo $SERVICE_ACCOUNT

export PROJECT_ID=$(gcloud config get-value project)

gcloud projects add-iam-policy-binding $PROJECT_ID \
--member="serviceAccount:$SERVICE_ACCOUNT" \
--role="roles/datafusion.serviceAgent"

gcloud projects get-iam-policy $PROJECT_ID \
--flatten="bindings[].members" \
--filter="bindings.members:$SERVICE_ACCOUNT" \
--format="table(bindings.role)"

gcloud projects add-iam-policy-binding $PROJECT_ID \
  --member="serviceAccount:$SERVICE_ACCOUNT" \
  --role="roles/iam.serviceAccountUser" \
  --condition=None


PROJECT_ID=$(gcloud config get-value project)
echo $PROJECT_ID

gcloud projects describe $PROJECT_ID

SERVICE_ACCOUNT_NAME="service-$(gcloud projects describe $PROJECT_ID --format="value(projectNumber)")@gcp-sa-datafusion.iam.gserviceaccount.com"
echo $SERVICE_ACCOUNT_NAME

gcloud projects add-iam-policy-binding $PROJECT_ID \
  --member="serviceAccount:$SERVICE_ACCOUNT_NAME" \
  --role="roles/dlp.admin"

gcloud projects get-iam-policy $PROJECT_ID \
  --flatten="bindings[].members" \
  --format="table(bindings.role)" \
  --filter="bindings.members:serviceAccount:$SERVICE_ACCOUNT_NAME"
```

## 🌐 Join our Community [Boost The Arcade](https://www.youtube.com/@BoostTheArcade) Don't Forget to like, share & subscribe
