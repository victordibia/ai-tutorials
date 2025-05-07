## Deploy the Azure Resources

The following resources will be created in the `rg-contoso-agent-workshop` resource group in your Azure subscription.

- An **Azure AI Foundry hub** 
- An **Azure AI Foundry project** 
- A **Serverless (pay-as-you-go) GPT-4o model deployment** named **gpt-4o (Global 2024-08-06)**. See pricing details [here](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/).

!!! Warning: You will need 140K TPM quota availability for the gpt-4o Global Standard SKU, not because the agent uses lots of tokens, but due to the frequency of calls made by the agent to the model. Review your quota availability in the [AI Foundry Management Center](https://ai.azure.com/managementCenter/quota)."

We have provided a bash script to automate the deployment of the resources required for the workshop. Alternatively, you may deploy resources manually using Azure AI Foundry portal. 

**Automated deployment**

The script `deploy.sh` deploys to the `eastus2` region by default; edit the file to change the region or resource names. To run the script, open the VS Code terminal and run the following command:

```bash
cd infra && ./deploy.sh
```

> !NOTE
> If you don't have permissions to execute the .sh script, make sure to change permissions before running it, by using:
> ```bash
> chmod +x ./deploy.sh
> ```

The deploy script generates the **.env** file, which contains the project connection string, model deployment name, and Bing connection name.

Your **.env** file should look similar to this but with your project connection string.

```python
MODEL_DEPLOYMENT_NAME="gpt-4o"
BING_CONNECTION_NAME="groundingwithbingsearch"
PROJECT_CONNECTION_STRING="<your_project_connection_string>"
```

**Manual deployment**

Alternatively, if you prefer not to use the `deploy.sh` script you can deploy the resources manually using the Azure AI Foundry portal as follows:

1. Navigate to the [Azure AI Foundry](https://ai.azure.com) web portal using your browser and sign in with your account.
2. Select **+ Create project**.

    - Name the project

        ```text
        agent-workshop
        ```

    - Create a new hub named

        ```text
        agent-workshop-hub
        ```

    - Select **Create** and wait for the project to be created.
3. From **My assets**, select **Models + endpoints**.
4. Select **Deploy Model / Deploy Base Model**.

    - Select **gpt-4o** from the model list, then select **Confirm**.
    - Name the deployment

        ```text
        gpt-4o
        ```

    - Deployment type: Select **Global Standard**.
    - Select **Customize**.
    - Model version: Select **2024-11-20**.
    - Tokens Per Minute Rate Limit: Select **140k**.
    - Select **Deploy**.

### Workshop Configuration

You'll need the project connection string to connect the agent app to the Azure AI Foundry project. You can find this string in the Azure AI Foundry portal in the Overview page for your Project `agent-workshop` (look in the Project details section).

Create the workshop configuration file with the following command:

```bash
cp src/python/workshop/.env.sample src/python/workshop/.env
```

Then edit the file `src/python/workshop/.env` to provide the Project Connection String.

## Selecting the Python Workspace

1. In Visual Studio Code, go to **File** > **Open Workspace from File**.
2. Replace the default path with the following:

    ```text
    /workspaces/build-your-first-agent-with-azure-ai-agent-service-workshop/.vscode/
    ```

3. Choose the file named **python-workspace.code-workspace** to open the workspace.

## Project Structure

Be sure to familiarize yourself with the key **folders** and **files** you’ll be working with throughout the workshop.

### The workshop folder

- The **main.py** file: The entry point for the app, containing its main logic.
- The **sales_data.py** file: The function logic to execute dynamic SQL queries against the SQLite database.
- The **stream_event_handler.py** file: Contains the event handler logic for token streaming.

### The shared folder

- The **files** folder: Contains the files created by the agent app.
- The **fonts** folder: Contains the multilingual fonts used by Code Interpreter.
- The **instructions** folder: Contains the instructions passed to the LLM.

![Lab folder structure](../media/project-structure-self-guided-python.png)



