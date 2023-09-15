Service account - To give the VM the permission to access different gcp services 

GCLOUD COMMANDS

1. Create a project

#Creating a VM instance
gcloud compute instances create mage-vm --machine-type=c2-standard-4 #compute-optimised instance
 
 Note: While creating this VM, 
            allow `HTTP,HTTPS traffic` to make access this VM on a public URL
            IAM - Applicaitons installed on the VM will use the VM's default service account(Compute engine default service account) to communicate with the Google Cloud API's
            Give this service account the required permissions according to the usecase:
                -Bigquery
                -Storage
                -`Compute Engine`


2. Enable required api's
gcloud services enable compute.googleapis.com
gcloud services enable storage.googleapis.com
gcloud services enable bigquery.googleapis.com
gcloud services enable iam.googleapis.com
#gcloud services list --project=igneous-fort-398700 #to list all the services or API's that are enabled

3.Schedule instance to be active only during business hours

    3.1. Create a resource policy
     gcloud compute resource-policies create instance-schedule office-hours --description="to operate in business hours only" --vm-start-schedule="09 * * *" --vm-stop-schedule="0 17 * * *" --timezone="UTC" --region=asia-southeast1 --initiation-date="2023-09-11T11:30:00.000Z" --end-date="2023-09-16T00:00:00.000Z" 

    3.2. Identify the default service account and the list of permissions it has (make sure it has permissions to start and stop the VM)
    <project-number>-compute@developer.gserviceaccount.com  -- Default Service Account

        -- list of service accounts
                gcloud iam service-accounts list
        -- Add a role to the service account (In this case roles required are compute.instances.start and compute.instances.stop, so we add compute.instances.admin)
                export project=$(gcloud info --format='value(config.project)')   #setting the project variable
                gcloud projects add-iam-policy-binding $project --role roles/compute.instanceAdmin.v1 --member serviceAccount:'1096978276183-compute@developer.gserviceaccount.com'

    To search all the resources in a project with number 123:
    $ gcloud asset search-all-resources --scope=projects/123

    3.3. Add this resource policy to the VM

4. Install these packages and applications on the VM


* `sudo apt-get update`: This command updates the list of packages that are available to install. This is important to do before installing any new packages, as it ensures that you are installing the latest versions of the packages.
* `sudo apt-get install python3-distutils`: This command installs the Python 3 distutils package. The distutils package is a set of tools that are used to build and distribute Python modules.
* `sudo apt-get install python3-apt`: This command installs the Python 3 apt module. The apt module is used to interact with the apt package manager.
* `sudo apt-get install wget`: This command installs the wget package. The wget package is used to download files from the internet.
* `wget https://bootstrap.pypa.io/get-pip.py`: This command downloads the get-pip.py script from the Python Package Index (PyPI).
* `sudo python3 get-pip.py`: This command installs the pip package. The pip package is a package manager for Python.


* **Commands to update the package list and install required packages:**
    * `sudo apt-get update`
    * `sudo apt-get install python3-distutils`
    * `sudo apt-get install python3-apt`
    * `sudo apt-get install wget`
* **Command to download and install the pip package:**
    * `wget https://bootstrap.pypa.io/get-pip.py`
    * `sudo python3 get-pip.py`


5. 
# Install Mage
sudo pip3 install mage-ai

# Install Pandas
sudo pip3 install pandas

# Install Google Cloud Library
sudo pip3 install google-cloud

sudo pip3 install google-cloud-bigquery



