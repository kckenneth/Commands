# Google Cloud Shell

Google Cloud Shell is the free-of-charge cloud shell service that comes with pre-installed google cloud (gloud) SDK, python, JAVA, and any essential apps commands. It also provides 5G persistent disk space. This cloud shell is recycled if you terminate. So intead of installing gcloud SDK into your local machine and communicate with your GCP account (which also requires you to have the internet), it's one step closer if you can do in your GCP account that provides you a shell service that can communicate with all the necessities. You can provision a new VM or create a storage bucket from your console. You can also do so by the cloud shell with a command. 

# Provision a new VM

Datalab is a shortcut to creating a new VM with a default specifications on the disk. 

```
datalab create <MyVM> --zone <ZONE>
```

`<MyVM>` = your choice  
`<ZONE>` = your regional zone, you can list the available zone by `gcloud compute zones list`. 


# Create a storage bucket (<a href=https://cloud.google.com/storage/docs/quickstart-gsutil target="_blank">details</a>)

```
REGION=us-east1
BUCKET=$(gcloud config get-value project)
TFVERSION=1.7

gsutil mb -l ${REGION} gs://${BUCKET}
```

# To transfer files from Compute Engine (GCP) 

- Need to establish ssh (private and public keys) in metada in console.cloud.google. Go to <a href="https://github.com/kckenneth/GCPsetup">GCP Setup</a> 

```
scp -i ~/.ssh/w266 kchen@xx.xx.xx.xx:/home/kchen/tf/TensorFlow-Tutorials/data/coco/transfer_values_val.pkl .
```
If you're using `gcloud compute` 
```
gcloud compute scp --recurse ./* kchen@xx.xx.xx.xxx:/home/kchen/tf/TensorFlow-Tutorials/data/coco/
```

# To shut down the project 

IAM & Admin --> Setting --> Select projects and shut down 
