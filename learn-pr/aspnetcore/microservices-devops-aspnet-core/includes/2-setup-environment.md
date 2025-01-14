In this unit, you'll use a script to deploy the existing *:::no-loc text="eShopOnContainers":::* app to Azure Kubernetes Service (AKS).

## Open the development environment and create the Azure resources

1. In a new browser window, fork the repository [github.com/MicrosoftDocs/mslearn-microservices-devops-aspnet-core](https://github.com/MicrosoftDocs/mslearn-microservices-devops-aspnet-core) to your own GitHub account. For instructions on forking, see [Forking Projects](https://guides.github.com/activities/forking).

    > [!NOTE]
    > If you wish to use GitHub Codespaces, create a new codespace using the `main` branch of your newly forked repository, and then skip to step 4.

1. From a new Visual Studio Code window, press **Ctrl+Shift+P** to open the command palette, and then search for and select **Dev Containers: Clone Repository in Container Volume**.

1. Provide your forked repository URL. Visual Studio Code creates your development container.

1. After the project loads in the container, expand the *deploy/k8s* directory. Right-click on the *k8s* directory and select **Open in Integrated Terminal**. This location contains the scripts you're going to use in this module. (Note: By default, Code will display *k8s* on the same line as *deploy* because *deploy* only contains the *k8s* subdirectory.)

    ![Screenshot of the explorer pane in Visual Studio Code. The context menu for the k8s folder is displayed, and Open in Integrated Terminal is selected.](../media/2-setup-environment/k8s-path.png)

1. In the new terminal pane, sign in to the Azure CLI. If using GitHub Codespaces, include the `--use-device-code` flag. If you are using Visual Studio Code, you may optionally omit the flag.

    ```azurecli
    az login --use-device-code
    ```

1. View your selected Azure subscription.

    ```azurecli
    az account show -o table
    ```

    If the wrong subscription is selected, select the correct one using the [az account set](/cli/azure/account#az-account-set) command.

1. Run the quickstart script:

    [!INCLUDE[Quickstart note](../../includes/microservices/quickstart.md)]

    ```bash
    ./quickstart.sh
    ```

    The preceding command runs a script that completes the following steps:

    * Provisions AKS and Azure Container Registry resources.
    * Deploys the containers to a fully managed Kubernetes service in Azure, known as AKS.
    * Displays connection information upon completion.

    > [!TIP]
    > This unit uses scripts to keep focus on the learning objectives. The script outputs colored text to indicate the commands being executed. You can inspect the script and the output to better understand the commands used.

The script deploys a modified version of the *:::no-loc text="eShopOnContainers":::* [reference app](https://github.com/dotnet-architecture/eshoponcontainers). The solution architecture of the app is pictured in the following diagram:

:::image type="content" source="../../media/microservices/eshop-architecture.png" alt-text="eShopOnContainers solution architecture diagram." border="true" lightbox="../../media/microservices/eshop-architecture.png":::

This module focuses on adding CI/CD for the coupon service depicted in the preceding diagram.
