# Prepare-Data-for-ML-APIs-on-Google-Cloud
Prepare Data for ML APIs on Google Cloud: Challenge Lab


Dataflow Lab:

Add storage Admin permission
Create BQ Dataset 
Bq mk <table name>

Create BQ table:
Gsutil cat gs://cloud-training/gsp323/lab.schema
Copy schema from terminal and use to create the table on console

Create a dataflow job on console using information on the table

Run a DataProc Job

First create a Cluster using the table config provided. Remember to Uncheck the Configure all instances to have only internal IP addresses.
SSH into the cluster CE and copy the /data.txt file into hdfs using
hdfs dfs -cp gs://cloud-training/gsp323/data.txt /data.txt
Create and run the Dataproc job on Console using table parameters provided



Google cloud Speech-to text API

Set project env variable:
export GOOGLE_CLOUD_PROJECT=$(gcloud config get-value core/project)
Create new service account
gcloud iam service-accounts create my-natlang-sa \
  --display-name "my natural language service account"
Create credentials and save to key.json file
gcloud iam service-accounts keys create ~/key.json \
  --iam-account my-natlang-sa@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com

Set Google_APPLICATION_CREDENTIALS environment variable to the full path of the credential json file that you have created:
export GOOGLE_APPLICATION_CREDENTIALS="/home/USER/key.json"

SSH into the Compute Engine
Run the NLP analysis request:
gcloud ml language analyze-entities --content="Old Norse texts portray Odin as one-eyed and long-bearded, frequently wielding a spear named Gungnir and wearing a cloak and a broad hat."  > result.json

Preview result
cat result.json

Upload file to CNL Location

Speech-to-Text API Lab
Create an API key
To create an API key, click Navigation menu > APIs & services > Credentials.
Then click Create credentials.
In the drop down menu, select API key.
Copy the key you just generated and click Close.
SSH into the provisioned compute engine
Add API key to env variable:
export API_KEY=<YOUR_API_KEY>

Create the request file
touch request.json
Open the request file:
nano request.json
Add the ff code to the request file:
{
  "config": {
      "encoding":"FLAC",
      "languageCode": "en-US"
  },
  "audio": {
      "uri":"Cloud speech location"
  }
}
Press control + x and then y and click enter to close the request.json file.
Call the Speech to text API
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json \
"https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}"
Save teh API response in a file:
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json \
"https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}" > result.json

Upload to the speech cloud location.




