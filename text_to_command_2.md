# Labs : Google Cloud Fundamentals: Getting Started with GKE

# Objectives
In this lab, you learn how to perform the following tasks:

    - Provision a Kubernetes cluster using Kubernetes Engine.

    - Deploy and manage Docker containers using kubectl.

# Steps:
1. Confirm that needed APIs are enabled with this command:

    ```
    gcloud services list --enabled
    ```

    - Result:Scroll down in the list of enabled APIs, and confirm that both of these APIs are enabled   

            Kubernetes Engine API
            Container Registry API

            

2. Start a Kubernetes Engine cluster

    - place the zone for the qwiklab project in a variable
        
        ```
        export MY_ZONE= us-central1-a
        ```
    
    - Start a Kubernetes cluster managed by Kubernetes Engine with the name webfrontend and 2 nodes with this command :

        ```
        gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
        ```

        NB: It takes several minutes to create a cluster as Kubernetes Engine provisions virtual machines 

    - check your installed version of Kubernetes with this command :
        ```
        kubectl version
        ```

3. Run and deploy a container

    - Launch a single instance of the nginx container with this command:
        ```
        kubectl create deploy nginx --image=nginx:1.17.10
        ```
    
    - View the pod running the nginx container with this command:
        ```
        kubectl get pods
        ```

    - Expose the nginx container to the Internet with this command:
        ```
        kubectl expose deployment nginx --port 80 --type LoadBalancer
        ```

    - View the new service:
        ```
        kubectl get services
        ```
    
    - Copy the displayed External IP address and paste in a browser tab
        - Result: This will display the default home page of the Nginx browse
        
    - Scale up the number of pods running on the service with this command:
        ```
        kubectl scale deployment nginx --replicas 3
        ```

    - Confirm that Kubernetes has updated the number of pods with this command:
        ```
        kubectl get pods
        ```

    - Confirm that your external IP address has not changed with this command:
        ```
        kubectl get services
        ```
    
    - Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.