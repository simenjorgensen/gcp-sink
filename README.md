Publish entities to GCP Pub/Sub

Sample system in Sesam:
```json
{
  "_id": "gcp-pubsub-sink",
  "type": "system:microservice",
  "docker": {
    "environment": {
      "GOOGLE_APPLICATION_CREDENTIALS": "credentials.json",
      "GOOGLE_APPLICATION_CREDENTIALS_CONTENT": { Pase your Credentials from GCP
      },
      "PAYLOAD_KEY": "<optional attribute which part of entity send as payload (if you don't want to pass whole entity)>",
      "PROJECT_ID": "<project id>"
    },
    "image": "<dockerhub-username>/<repository>:<tag>",
    "port": 5000
  },
  "verify_ssl": true
}


Sample output pipe:
{
  "_id": "customer-meter-endpoint",
  "type": "pipe",
  "source": {
    "type": "dataset",
    "dataset": "customer-meters"
  },
  "sink": {
    "type": "json",
    "system": "gcp-pubsub-sink",
    "url": "/<topic_id>"
  },
  "pump": {
    "cron_expression": "0 0 1 1 ?"
  }
}

