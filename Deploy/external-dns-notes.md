# Azure Configuration for External-DNS

## Step 1: Create `azure.json` file

Create a file named `azure.json` with the following content:

```json
{
  "tenantId": "01234abc-de56-ff78-abc1-234567890def",
  "subscriptionId": "01234abc-de56-ff78-abc1-234567890def",
  "resourceGroup": "MyDnsResourceGroup",
  "useManagedIdentityExtension": true,
  "userAssignedIdentityID": "01234abc-de56-ff78-abc1-234567890def"
}

## Step 2: Create Kubernetes Secret
Use the following command to create a Kubernetes secret named azure-config-file using the azure.json file:

```bash
      kubectl create secret generic azure-config-file --namespace "default" --from-file /home/azureuser/azure.json
```

## Step 3: Add Bitnami Helm Repository
Add the Bitnami Helm repository to your Helm setup (if not already added):
```bash
      helm repo add bitnami https://charts.bitnami.com/bitnami
```

## Step 4: Update Helm Repositories
- Update the Helm repositories to get the latest charts:
  ```bash
      helm repo update
  ```
## Step 5: Install External-DNS Using Helm
- Install the external-dns chart from the Bitnami repository. Replace <namespace> with your desired Kubernetes namespace (e.g., default, kube-system), and make sure to provide a values.yaml file for configuration:
  ```bash
        helm install external-dns bitnami/external-dns --namespace <namespace> --create-namespace -f values.yaml
## Step 6: Uninstall the External-DNS Release
To uninstall the external-dns release, use the following command:

- List all Helm releases:
    ```bash
        helm list
    ```
- Uninstall external-dns:
    ```bash
        helm uninstall external-dns -n <namespace>
    ```
Step 7: Remove a Helm Repository
To remove a repository from Helm, first list your repos and then remove the desired one:
- List all repositories:
  ```bash
        helm repo list
  ```
- Remove the Bitnami repository (or any other repo):
  ```bash
        helm repo remove bitnami
  ```
