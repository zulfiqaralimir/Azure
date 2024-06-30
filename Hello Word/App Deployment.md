### Step 1: Log In to Azure

Open your command prompt or terminal and log in to your Azure account:

```
az login

```

### Step 2: Build the Docker Image Locally

Navigate to your project directory where your Dockerfile is located and build the Docker image:

```
cd C:\\azure_cloud\\hello_world\\azure_hello_world
docker build -t helloworldenv947d9e.azurecr.io/azurehelloworld:latest .

```

### Step 3: Log in to Azure Container Registry (ACR)

Log in to your ACR to push the Docker image:

```
az acr login --name helloworldenv947d9e

```

### Step 4: Push the Docker Image to ACR

Push your Docker image to ACR:

```
docker push helloworldenv947d9e.azurecr.io/azurehelloworld:latest

```

### Step 5: Create the Container App Environment

Create the container app environment if it doesn't already exist:

```
az containerapp env create --name hello-world-env --resource-group hello-world-env --location southeastasia

```

### Step 6: Create the Container App

Create the container app using the image you pushed to ACR:

```
az containerapp create --name azurehelloworldapp --resource-group hello-world-env --environment hello-world-env --image helloworldenv947d9e.azurecr.io/azurehelloworld:latest --target-port 8000 --ingress external --registry-server helloworldenv947d9e.azurecr.io --cpu 0.5 --memory 1.0Gi

```

### Step 7: Retrieve the FQDN of Your Container App

Get the Fully Qualified Domain Name (FQDN) of your container app

```
az containerapp show --name azurehelloworldapp --resource-group hello-world-env --query properties.configuration.ingress.fqdn -o tsv

```

This command will return the FQDN of your container app. The `-o tsv` option ensures that the output is in plain text format.

### Step 8: Access the Container App in the Browser
Open your web browser and navigate to the URL provided by the FQDN. For example, if the FQDN returned is `azurehelloworldapp.southeastasia.azurecontainerapps.io`, you would open:

```
<http://azurehelloworldapp.southeastasia.azurecontainerapps.io>

```

### Complete Workflow Summary

1. **Log in to Azure**:
    
    ```
    az login
    
    ```
    
2. **Build the Docker Image**:
    
    ```
    cd C:\\Users\\wania\\OneDrive\\Documents\\Q5\\azure_cloud\\hello_world\\azure_hello_world
    docker build -t helloworldenv947d9e.azurecr.io/azurehelloworld:latest .
    
    ```
    
3. **Log in to ACR**:
    
    ```
    az acr login --name helloworldenv947d9e
    
    ```
    
4. **Push the Docker Image to ACR**:
    
    ```
    docker push helloworldenv947d9e.azurecr.io/azurehelloworld:latest
    
    ```
    
5. **Create the Container App Environment**:
    
    
    ```
    az containerapp env create --name hello-world-env --resource-group hello-world-env --location southeastasia
    
    ```
    
6. **Create the Container App**:
    
    ```
    az containerapp create --name azurehelloworldapp --resource-group hello-world-env --environment hello-world-env --image helloworldenv947d9e.azurecr.io/azurehelloworld:latest --target-port 8000 --ingress external --registry-server helloworldenv947d9e.azurecr.io --cpu 0.5 --memory 1.0Gi
    
    ```
    
7. **Retrieve the FQDN**:
    
    ```
    az containerapp show --name azurehelloworldapp --resource-group hello-world-env --query properties.configuration.ingress.fqdn -o tsv
    
    ```
    
8. **Access the App in the Browser**:
Open your web browser and go to:
    
    ```
    http://<your-fqdn>
    
    ```
    

By following these detailed steps, you will be able to deploy your container app to Azure and access it through your web browser. If you encounter any issues at any step, please let me know, and I can provide further assistance.

## **Q: Where to get ACR name?**

To get the ACR (Azure Container Registry) name, you can use the Azure CLI to list your existing container registries. Here are the steps:

### Step 1: Log In to Azure

First, log in to your Azure account using the Azure CLI:

```bash
az login

```

### Step 2: List Azure Container Registries

To list all the Azure Container Registries in your subscription, use the following command:

```
az acr list --output table

```

This command will output a table with the names of your Azure Container Registries, along with other details such as resource group and location.

### Step 3: Identify the ACR Name

From the output, identify the name of the container registry you want to use. The name is listed under the `NAME` column.

### Example

```
$ az acr list --output table
Name                ResourceGroup     Location    Sku       LoginServer
------------------  ----------------  ----------  --------  --------------------------------
helloworldenv947d9e  hello-world-env  eastus      Standard  helloworldenv947d9e.azurecr.io

```

In this example, `helloworldenv947d9e` is the name of the Azure Container Registry.

### Step 4: Use the ACR Name

Now that you have identified the ACR name, you can use it in your Docker commands and Azure CLI commands.
