# Apache Airflow Installation on Local
##  Description
This file contains the steps for installing Apache-Airflow locally using Windows Sub-system Linux (WSL)
## Install Linux on Windows with Windows Sub-system Linux (WSL)
### Prerequisites
You must be running Windows 10 version 2004 and higher (Build 19041 and higher) or Windows 11 to use the commands below.
### Install WSL Command
Open PowerShell or Windows Command Prompt in administrator mode by right-clicking and selecting "Run as administrator", enter the wsl --install command, then restart your machine.  

``` wsl --install```
### Integrating WSL terminal with VS Code
1. Install the WSL Extension for VSCode  

Open VSCode.  

Go to the Extensions view by clicking on the Extensions icon in the Activity Bar on the side of the window.  

Search for "Remote - WSL" and install it. This extension allows you to open a WSL session directly in VSCode.  


2. Open the WSL Terminal in VSCode  

Once the "Remote - WSL" extension is installed:  

Click on the green button in the bottom-left corner of VSCode that says >< or Open Remote Window.  

Select "Remote-WSL: New Window" from the options. This will open a new VSCode window that is connected to your WSL environment.  

## Creating Virtual Environment
Run ```sudo apt update``` command in WSL terminal to update the Ubuntu version  

Navigate to the project folder by running the command ```cd /mnt/<path-to-your-project>```  

Create the virtual environment by running the command ```python3 -m venv airflowvenv2```  

(replace airflowvenv2 with your desired name for the environment)  

Activate the virtual environment by running the command ```source airflowvenv/bin/activate```



## Apache Airflow installation
### To Install Apache Airflow run below command in WSL terminal
You can install Apache Airflow using the pip command. It’s a good practice to specify the version of Airflow you want to install.  

``` pip install "apache-airflow[celery]==2.10.3" --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.10.3/constraints-3.8.txt" ```  

### Initialize the Airflow Database
Apache Airflow requires a backend database to store metadata (such as task states). The default database used is SQLite, which is good for testing and development.  

To initialize the airflow database run this command ```airflow db init```  

This will create the necessary tables and other database configurations in the default SQLite database located in ~/airflow/airflow.db.
### Create a User for the Web UI
Airflow comes with a web-based user interface (UI) for managing workflows. You need to create an admin user to access this UI.  

```
airflow users create \
             --username admin \
             --password admin \
             --firstname First \
             --lastname Last \
             --role Admin \
             --email admin@example.com
```  

### Start Airflow Web Server
Launch the Airflow web server to access the UI by running below command  

``` airflow webserver --port 8080```  

### Start Airflow Scheduler
In a separate terminal window, start the scheduler by running below command  

``` airflow scheduler ```  

Access the Airflow Web UI: Open a browser and go to http://localhost:8080/ to access the Airflow UI. Log in with the username and password you created

