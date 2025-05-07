## Introduction

This workshop is designed to teach you about the Azure AI Agents Service and the associated SDK. It consists of multiple labs, each highlighting a specific feature of the Azure AI Agents Service. The labs are meant to be completed in order, as each one builds on the knowledge and work from the previous lab.

## Prerequisites

1. Access to an Azure subscription. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.
1. You need a GitHub account. If you don’t have one, create it at [GitHub](https://github.com/join).

## Open the Workshop

The preferred way to run this workshop is using GitHub Codespaces. This option provides a pre-configured environment with all the tools and resources needed to complete the workshop. Alternatively, you can open the workshop locally using a [Visual Studio Code Dev Container](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers). In this case, you would need to clone the [solution repo](https://github.com/microsoft/build-your-first-agent-with-azure-ai-agent-service-workshop) from its remote location.

Select **Open in GitHub Codespaces** to open the project in GitHub Codespaces.

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/microsoft/build-your-first-agent-with-azure-ai-agent-service-workshop)

!!! Warning: Building the Codespace will take several minutes. You can continue reading the instructions while it builds.

## Authenticate with Azure

You need to authenticate with Azure so the agent app can access the Azure AI Agents Service and models. Follow these steps:

1. Ensure the Codespace has been created.
1. In the Codespace, open a new terminal window by selecting **Terminal** > **New Terminal** from the **VS Code menu**.
1. Run the following command to authenticate with Azure:

    ```shell
    az login --use-device-code
    ```

    !!! note
        You'll be prompted to open a browser link and log in to your Azure account. Be sure to copy the authentication code first.

        1. A browser window will open automatically, select your account type and click **Next**.
        2. Sign in with your Azure subscription **Username** and **Password**.
        3. **Paste** the authentication code.
        4. Select **OK**, then **Done**.

    !!! warning
        If you have multiple Azure tenants, then you will need to select the appropriate tenant when authenticating.

        ```shell
        az login --use-device-code --tenant <tenant_id>
        ```

1. Next, select the appropriate subscription from the command line.
1. Leave the terminal window open for the next steps.

## Select Workshop Programming Language

The workshop is available in both [Python](./Python/) and [C#](./C#/). Please find the following instructions in the corresponding folders.

> !NOTE
> If you are running this lab as a guided workshop at a community event, please make sure to double check with the workshop lead which programming language to choose.