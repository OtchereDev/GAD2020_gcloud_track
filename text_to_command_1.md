# Labs: Google Cloud Fundamentals: Getting Started with Compute Engine

## Objectives
In this lab, you will learn how to perform the following tasks:

    - Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

    - Create a Compute Engine virtual machine using the gcloud command-line interface.

    - Connect between the two instances.

# Steps:
1. Create compute engine virtual machine using the Google cloud console.

    ```gcloud compute instances create "my-vm-1" 
    --machine-type "n1-standard-1" 
    --image-project "debian-cloud" 
    --image "debian-9-stretch-v20190213" 
    --subnet "default"
    ```

    ```
    gcloud compute firewall-rules create allow-http --action=ALLOW --destination=INGRESS --rules=http:80 --target-tag=http
    ```

2. Create a compute engine virtual machine using the gcloud commandline.

    ```
    gcloud config set compute/zone us-central1-b

    gcloud compute instances create "my-vm-2" 
    --machine-type "n1-standard-1" 
    --image-project "debian-cloud" 
    --image "debian-9-stretch-v20190213" 
    --subnet "default"

    ```

3. connect between the two instance
    1. Use the ping command to confirm my-vm-2 can reach my-vm-1:
        - Connect to my-vm-2:
            ```
            gcloud compute ssh my-vm-2
            ```
        - Ping my-vm-1 from my-vm-2:
            ``` 
            ping -c 4 my-vm-1
             ```
        - Use the ssh command to open prompt on my-vm-1 from my-vm-2:
            ``` 
            ssh my-vm-1
             ```  
        - At the command prompt on my-vm-1, install the ngix web server:
            ``` 
            sudo nano /var/www/html/index.nginx-debian.html 
            ```
        - Add text like his and replace YOUR_NAME with your name:
            ```
            Hi from OLIVER OTCHERE
            ```
        - Exit the editor and confirm that the web server is servig your new page. At the command on my-vm-1, excute this command:
            ```
             curl http://localhost/
            ```
        - To exit the command prompt on my-vm-1, excute this command:
            ```
            exit
            ```
        - To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt of my-vm-2, excute this command
            ```
             curl http://my-vim-1/
            ```
    
    2. Now get the externam IP of the my-vm-1 instance from this command:
        ```
        gcloud compute instance list --zone us-central1-a
        ```
    
    3. Paste the copied ip of my-vim-1 into a new browser tab and hit enter