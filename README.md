## ETL Pipeline with MAGE and GCP

In this repo, I documented the procedures I took to set up the ETL pipeline using MAGE. 

1. Set up your GCP account

You can sign up a GCP account with $400 free credit which is enough for your personal project. Then the first thing you need to do is creating a VM instance. There are tons of tutorials that show you how to do this so I'll skip this part.

2. save the ssh key to ~/.ssh folder of your local computer, and then you can run `ssh the_name_of_your_vm_instance` to connect to your VM instance on cloud.

I'm using visual studio to work on my VM. To do that, you need to install the extension called "Remote SSH" in your visual studio.

3. Install miniconda and docker inside the VM instance.

4. Create service account, then create key (json) and rename it if you wish. Put my-creds.json to somewhere in the virtual machine.

5. Navigate to the folder where your docker-compose.yml file exists. Run `docker-compose build` and then `docker-compose up -d`. You will have MAGE AI and Postgres running after finishing this step.

6. Forward port 6789 in your VS code, then open the browser and enter "localhost:6789" to navigate to MAGE UI. 

8. Create pipelines inside your project. 

9. Create a BigQuery dataset for your project (I was using Terraform to do this, but you can also do it manually).

10. Make sure that my-creds.json file does exist in the container under `/home/src/` folder. You can check it using the terminal with MAGE UI.

11. Change the path of the gcp key in the "io_config.yml" file.

12. Everytime the instance is shut down and then restart, the external IP address changes so you need to update that in the config file in the .ssh file

13. The `.env` file should exist in the same folder as the docker-compose.yml file

14. Important note!!! You need to make sure that the container in which you are running your MAGE AI is the same one that your MAGE UI is running. If it's not, kill everything that was running on port 6789 because they might be stale and then rerun docker-compose build and docker-compose up

### Mage repository structure

We just initialized a new mage repository. It will be present in your project under the name `my_de_test_project`. If you change the varable `PROJECT_NAME` in the `.env` file, it will be named whatever you set it to.

The Mage repository should have the following structure:

```
.
├── mage_data
│   └── my_de_test_project
├── my_de_test_project
│   ├── __pycache__
│   ├── charts
│   ├── custom
│   ├── data_exporters
│   ├── data_loaders
│   ├── dbt
│   ├── extensions
│   ├── interactions
│   ├── pipelines
│   ├── scratchpads
│   ├── transformers
│   ├── utils
│   ├── __init__.py
│   ├── io_config.yaml
│   ├── metadata.yaml
│   └── requirements.txt
├── Dockerfile
├── README.md
├── dev.env
├── docker-compose.yml
└── requirements.txt
```


