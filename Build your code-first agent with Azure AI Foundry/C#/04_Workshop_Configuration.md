## Deploy the Azure Resources

The following resources will be created in the `rg-contoso-agent-workshop` resource group in your Azure subscription.

- An **Azure AI Foundry hub** named **agent-wksp**
- An **Azure AI Foundry project** named **Agent Service Workshop**
- A **Serverless (pay-as-you-go) GPT-4o model deployment** named **gpt-4o (Global 2024-11-20)**. See pricing details [here](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/).
- A **Grounding with Bing Search** resource. See the [documentation](https://learn.microsoft.com/azure/ai-services/agents/how-to/tools/bing-grounding) and [pricing](https://www.microsoft.com/en-us/bing/apis/grounding-pricing) for details.

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

**Automated deployment**
The deploy script generates the **.env** file, which contains the project connection string, model deployment name, and Bing connection name.

Your **.env** file should look similar to this but with your project connection string.

The automated deployment script stores project variables securely by using the Secret Manager feature for [safe storage of app secrets in development in ASP.NET Core](https://learn.microsoft.com/aspnet/core/security/app-secrets).

You can view the secrets by running the following command:

```bash
dotnet user-secrets list
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

1. Open a new terminal window in VS Code.
2. Run the following command to set the C# project path $CSHARP_PROJECT_PATH variable:

    ```bash
    CSHARP_PROJECT_PATH="src/csharp/workshop/AgentWorkshop.Client/AgentWorkshop.Client.csproj"
    ```
3. Run the following command to set the [ASP.NET Core safe secret](https://learn.microsoft.com/aspnet/core/security/app-secrets) for the project connection string:

    !!! warning "Replace `<your_project_connection_string>` with the actual connection string"

    ```bash
    dotnet user-secrets set "ConnectionStrings:AiAgentService" "<your_project_connection_string>" --project "$CSHARP_PROJECT_PATH"
    ```

4. Run the following command to set the [ASP.NET Core safe secret](https://learn.microsoft.com/aspnet/core/security/app-secrets) for the model deployment name:

    ```bash
    dotnet user-secrets set "Azure:ModelName" "gpt-4o" --project "$CSHARP_PROJECT_PATH"
    ```

## Selecting the C# Workspace

1. In Visual Studio Code, go to **File** > **Open Workspace from File**.
2. Replace the default path with the following:

    ```text
    /workspaces/build-your-first-agent-with-azure-ai-agent-service-workshop/.vscode/
    ```

3. Choose the file named **csharp-workspace.code-workspace** to open the workspace.

## Project Structure

Be sure to familiarize yourself with the key **folders** and **files** you’ll be working with throughout the workshop.

### The workshop folder

- The **Lab1.cs, Lab2.cs, Lab3.cs** files: The entry point for each lab, containing its agent logic.
- The **Program.cs** file: The entry point for the app, containing its main logic.
- The **SalesData.cs** file: The function logic to execute dynamic SQL queries against the SQLite database.

### The shared folder

- The **files** folder: Contains the files created by the agent app.
- The **fonts** folder: Contains the multilingual fonts used by Code Interpreter.
- The **instructions** folder: Contains the instructions passed to the LLM.

![Lab folder structure](../media/project-structure-self-guided-csharp.png)
