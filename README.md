# Microsoft Copilot Studio ❤️ MCP

Microsoft Copilot Studio ❤️ MCP 랩에 오신 것을 환영합니다. 이 랩에서는 MCP 서버를 배포하는 방법과 Microsoft Copilot Studio에 추가하는 방법을 학습합니다.

## ❓ What is MCP?

[Model Context Protocol (MCP)](https://modelcontextprotocol.io/introduction)는 애플리케이션이 LLM에 컨텍스트를 제공하는 방법을 표준화하는 오픈 프로토콜입니다. 이 프로토콜은 [Anthropic](https://www.anthropic.com/)에서 정의했습니다. MCP는 AI 모델을 다양한 데이터 소스와 도구에 연결하는 표준화된 방법을 제공합니다. 이를 통해 제작자는 기존 지식 서버와 API를 Copilot Studio에 직접 통합할 수 있습니다.

현재, Copilot Studio는 Tools(도구)만 지원합니다. 현재 기능에 대한 자세한 내용은 [aka.ms/mcsmcp](https://aka.ms/mcsmcp)를 참고하세요. 

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8e074fea-dcb6-49f5-8bc2-e6d476b42e94" />

> 이미지와 관련된 원본은 [여기](https://www.claudemcp.com/ko/blog/mcp-vs-api)에서 참고할 수 있습니다.

## 🆚 MCP vs Connectors

✅ MCP는 언제 사용하나요?

AI 모델과 다양한 데이터 소스 또는 도구를 표준화된 방식으로 연결해야 할 때 사용합니다.
예를 들어, Copilot Studio에서 외부 API나 지식 서버를 직접 통합하고 싶을 때 MCP가 적합합니다.
MCP는 Model Context Protocol을 기반으로 하며, LLM이 컨텍스트를 이해하고 활용할 수 있도록 돕습니다.


✅ 커넥터는 언제 사용하나요?

Power Platform에서 기존의 **데이터 소스(예: Dynamics 365, SharePoint, SQL 등)**와 연결할 때 사용합니다.
커넥터는 비즈니스 애플리케이션 통합에 특화되어 있으며, 데이터 작업과 워크플로우 자동화에 강점이 있습니다.


✅ MCP가 커넥터를 대체하나요?

아니요. MCP는 커넥터를 대체하지 않습니다.
MCP 서버는 **커넥터 인프라**를 기반으로 제공되므로, 두 기술은 함께 사용됩니다.
MCP 서버는 커넥터 인프라를 활용해 엔터프라이즈 보안 및 거버넌스 제어를 적용할 수 있습니다:

- V-net 통합 기능: https://learn.microsoft.com/power-platform/admin/vnet-support-overview
- Power Platform DLP 정책: https://learn.microsoft.com/power-platform/admin/wp-data-loss-prevention
- Custom Connector 보호: https://learn.microsoft.com/connectors/custom-connectors/#2-secure-your-api

따라서 **MCP + 커넥터** = 더 강력한 통합입니다.

## ⚙️ Prerequisites

- Visual Studio Code installed ([link](https://code.visualstudio.com/download))
- Node v22 (ideally installed via [nvm for Windows](https://github.com/coreybutler/nvm-windows) or [nvm](https://github.com/nvm-sh/nvm))
- Git installed ([link](https://git-scm.com/downloads))
- Docker installed ([link](http://aka.ms/azure-dev/docker-install))
- Azure Developer CLI installed ([link](https://learn.microsoft.com/azure/developer/azure-developer-cli/install-azd))
- Azure Subscription (with payment method added)
- GitHub account
- Copilot Studio trial or developer account

## ➕ 템플릿 기반의 신규 깃럽 리포 생성하기

1. https://github.com/microsoft/mcsmcp 깃헙 리포 접속합니다.
1. `Use this template` 선택합니다.
   <img width="1710" height="516" alt="image" src="https://github.com/user-attachments/assets/35c54192-462b-4feb-b199-d586963b631f" />

3. `Create a new repository` 선택합니다.

    <img width="357" height="237" alt="image" src="https://github.com/user-attachments/assets/b614bb38-b73e-441d-9e0b-172addb1b255" />


1. 알맞은 `Owner`를 선택합니다. (보통은 다음과 같이 본인으로 지정)
   <img width="806" height="275" alt="image" src="https://github.com/user-attachments/assets/27800d87-c2ee-4e44-ac59-23ac88cf703a" />

1. `Repository name`을 입력합니다. 여기서는 **mcsmcp-kr** 입력합니다.
1. 필요하다면 `Description` 항목에 비고를 입력합니다.
1. `Private`을 선택합니다.
1.  `Create repository` 선택합니다.
   
    이 작업은 시간이 조금 걸립니다. 완료된 이후에 새롭게 생성된 리포지토리로 redirect 됩니다.

## ⚖️ 선택: 서버를 로컬로 실행하거나 Azure에 배포

이제는 선택할 수 있습니다! :) 서버를 로컬로 동작시키거나, Azure에 배포할 수 있습니다.
다만, 두 가지 모두에 대해 몇 가지 단계를 거쳐야 합니다.

1. 아래 명령어를 기반으로 현재 깃헙 리포지토리를 클론합니다. ( `{account}`를 사용자의 깃헙 계정 이름으로 변경)

`git clone https://github.com/{account}/mcsmcp-kr.git`

> 예시: 저는 git clone https://github.com/ChangJu-Ahn/mcsmcp-KR으로 입력했습니다.

<img width="1039" height="383" alt="image" src="https://github.com/user-attachments/assets/946f336b-6f83-461a-9039-f2e6f5bbb68d" />

2. 비주얼 스튜디오 코드를 실행하고, 리포지토리를 클론해 둔 폴더경로를 `open` 합니다.
   
   <img width="378" height="379" alt="image" src="https://github.com/user-attachments/assets/b4f7a583-e0c6-4763-8564-1519e09b88b3" />
   
4. 터미널을 열고, 클론된 폴더 경로로 이동합니다.
   
   <img width="618" height="378" alt="image" src="https://github.com/user-attachments/assets/6f3f14a4-ea1a-4b41-8072-d52e9f3c4fc6" />

### 🏃‍♀️ Run the MCP Server Locally

1. 터미널 창에서 `npm install` 를 입력합니다.
1. 그리고 `npm run build && npm run start` 를 입력합니다.

    <img width="389" height="137" alt="image" src="https://github.com/user-attachments/assets/008424dd-9e43-4b68-9c19-39bc0c23938f" />


1.  터미널 옆에 탭 창에서 `PORTS` 버튼을 누릅니다.

    <img width="407" height="141" alt="image" src="https://github.com/user-attachments/assets/88614f7a-7e88-44a4-a93a-8eba2a420b17" />


1. 초록색의 `Forward a Port` 버튼을 누릅니다.

   <img width="421" height="101" alt="image" src="https://github.com/user-attachments/assets/a7cbfb0d-8217-4aa6-8a6d-c2ea730d12eb" />


    ![Image of VS Code where the PORTS tab is open and the green `Forward a Port` button is highlighted](./assets/vscode-terminal-ports-forward.png)

1. Enter `3000` as the port number (this should be the same as the port number you see when you ran the command in step 5). You might be prompted to sign in to GitHub, if so please do this, since this is required to use the port forwarding feature.
1. Right click on the row you just added and select `Port visibility` > `Public` to make the server publicly available
1. Ctrl + click on the `Forwarded address`, which should be something like: `https://something-3000.something.devtunnels.ms`
1. Select `Copy` on the following pop-up to copy the URL

    ![View of the PORTS setup with highlighted the port, the forwarded address and the visibility](./assets/vscode-terminal-ports-setup.png) 

1. Open to the browser of your choice and paste the URL in the address bar, type `/mcp` behind it and hit enter

If all went well, you will see the following error message:

```json
{"jsonrpc":"2.0","error":{"code":-32000,"message":"Method not allowed."},"id":null}
```

Don't worry - this error message is nothing to be worried about!

### 🌎 Deploy to Azure

> [!IMPORTANT]
> As listed in the [prerequisites](#️-prerequisites), the [Azure Developer CLI ](https://learn.microsoft.com/azure/developer/azure-developer-cli/install-azd) needs to be installed on your machine for this part.

Make sure to login to Azure Developer CLI if you haven't done that yet.

```azurecli
azd auth login
```

> [!WARNING]  
> After running `azd up`, you will have an MCP Server running on Azure that is publicly available. Ideally, you don't want that. Make sure to run `azd down` after finishing the lab to delete all the resources from your Azure subscription. Learn how to run `azd down` by going to [this section](#-remove-the-azure-resources). 

Run the following command in the terminal:

```azurecli
azd up
```

For the unique environment name, enter `mcsmcplab` or something similar. Select the Azure Subscription to use and select a value for the location. After that, it will take a couple of minutes before the server has been deployed. When it's done - you should be able to go to the URL that's listed at the end and add `/mcp` to the end of that URL.

![Azd deploy server output](./assets/azd-deploy-server.png)

You should again see the following error:

```json
{"jsonrpc":"2.0","error":{"code":-32000,"message":"Method not allowed."},"id":null}
```

## 👨‍💻 Use the Jokes MCP Server in Visual Studio Code / GitHub Copilot

To use the Jokes MCP Server, you need to use the URL of your server (can be either your devtunnel URL or your deployed Azure Container App) with the `/mcp` part at the end and add it as an MCP Server in Visual Studio Code.

1. Press either `ctrl` + `shift` + `P` (Windows/Linux) or `cmd` + `shift` + `P` (Mac) and type `MCP`
1. Select `MCP: Add Server...`
1. Select `HTTP (HTTP or Server-Sent Events)`
1. Paste the URL of your server in the input box (make sure `/mcp` in the end is included)
1. Press `Enter`
1. Enter a name for the server, for instance `JokesMCP`
1. Select `User Settings` to save the MCP Server settings in your user settings

    This will add an MCP Server to your `settings.json` file. It should look like this:
    ![settings.json file](./assets/settings.png)

1. Open `GitHub Copilot`
1. Switch from `Ask` to `Agent`
1. Make sure the `JokesMCP` server actions are selected when you select the tools icon:

    ![Tools menu in GitHub Copilot](./assets/tools-menu.png)

1. Ask the following question:

    ```text
    Get a chuck norris joke from the Dev category
    ```

This should give you a response like this:

![Screenshot of question to provide a joke from the dev category and the answer from GitHub Copilot](./assets/github-copilot-get-joke.png)

Now you have added the `JokesMCP` server to Visual Studio Code!

## 👨‍💻 Use the Jokes MCP Server in Microsoft Copilot Studio

**Import the Connector**

1. Go to https://make.preview.powerapps.com/customconnectors (make sure you’re in the correct environment) and click **+ New custom connector**. 
1. Select `Import from GitHub`
1. Select `Custom` as **Connector Type**
1. Select `dev` as the **Branch**
1. Select `MCP-Streamable-HTTP` as the **Connector**
1. Select `Continue`

    ![View of the import from GitHub section](./assets/import-from-github.png)

1. Change the **Connector Name** to something appropriate, like for instance `Jokes MCP` 
1. Change the **Description** to something appropriate
1. Paste your root URL (for instance `something-3000.something.devtunnels.ms` or `something.azurecontainerapps.io`) in the **Host** field
1. Select **Create connector** 

> [!WARNING]  
> You may see a warning and an error upon creation – it should be resolved soon - but you can ignore it for now.

11. Close the connector


**Create an agent and add the MCP server as a tool**

1. Go to https://copilotstudio.preview.microsoft.com/
1. Select the environment picker at the top right corner
1. Select the right environment (the environment with the `Get new features early` toggle switched on)
1. Select `Create` in the left navigation
1. Select the blue `New agent` button

    ![New agent](./assets/newagent.png)

1. Select the `Configure` tab on the left

    ![Configure](./assets/configure.png)

1. Change the name to `Jokester`
1. Add the following `Description`

    ```text
    A humor-focused agent that delivers concise, engaging jokes only upon user request, adapting its style to match the user's tone and preferences. It remains in character, avoids repetition, and filters out offensive content to ensure a consistently appropriate and witty experience.
    ```

1. Add the following `Instructions`

    ```text
    You are a joke-telling assistant. Your sole purpose is to deliver appropriate, clever, and engaging jokes upon request. Follow these rules:
    
    * Respond only when the user asks for a joke or something related (e.g., "Tell me something funny").
    * Match the tone and humor preference of the user based on their input—clean, dark, dry, pun-based, dad jokes, etc.
    * Never break character or provide information unrelated to humor.
    * Keep jokes concise and clearly formatted.
    * Avoid offensive, discriminatory, or NSFW content.
    * When unsure about humor preference, default to a clever and universally appropriate joke.
    * Do not repeat jokes within the same session.
    * Avoid explaining the joke unless explicitly asked.
    * Be responsive, witty, and quick.
    ```

1. Select `Continue` on the top right

    ![Click continue to create agent](./assets/continue.png)

1. Enable Generative AI `Orchestration`

    ![Turn on orchestration](./assets/turnonorchestration.png)

1. Disable general knowledge in the `Knowledge` section

    ![Turn off general knowledge](./assets/turnoffgeneralknowledge.png)

1. Select `Tools` in the top menu
 
    ![Tools](./assets/tools.png)

1. Select `Add a tool`

    ![Add a tool](./assets/addatool.png)

1. Select the `Model Context Protocol` tab to filter all the Model Context Protocol Servers (see number 1 in the screenshot below)

1. Select the `Jokes MCP` server (see number 2 in the screenshot below)

    ![MCP](./assets/mcpsteps.png)

1. Create a new connection by selecting the `Not connected` and **Create new Connection**

    ![Action and connection](./assets/create-connection-action.png)

1. Select `Create`

    ![Create connection](./assets/create-connection-action-create.png)

1. Select `Add to agent` to add the tool to the agent

    ![Add tool to agent](./assets/add-tool-to-agent.png)

1. Select the `refresh icon` in the `Test your agent` pane

    ![Refresh testing pane](./assets/refreshtestingpane.png)

1. In the `Test your agent` pane send the following message:

    ```text
    Can I get a Chuck Norris joke?
    ```
  
    This will show you message that additional permissions are required to run this action. This is because of the user authentication in the action wizard.

1. Select `Connect`

    ![Additional permissions](./assets/additionalpermissions.png)
  
    This will open a new window where you can manage your connections for this agent.

1. Select `Connect` next to the `JokesMCP`

    ![Connect to JokesMCP](./assets/connect.png)

1. Wait until the connection is created and select `Submit`

    ![Pick a connection](./assets/submitconnection.png)

1. The connection should now be connected, so the status should be set to `Connected`

    ![Status connected](./assets/connected.png) 

1. Close the manage your connections tab in your browser

    Now you should be back in the Jokester agent screen.

1. Select the `refresh icon` in the `Test your agent` pane

    ![Refresh testing pane](./assets/refreshtestingpane.png)

1. In the `Test your agent` pane send the following message:

    ```text
    Can I get a Chuck Norris joke?
    ```

    This will now show a Chuck Norris joke - instead of the additional permissions. If that's not the case - you probably have missed the [prerequisite](#️-prerequisites) that the environment needs to have the `get new features early` toggle on.

    ![Chuck Norris joke](./assets/chucknorrisjoke.png)

1. In the `Test your agent` pane send the following message:

    ```text
    Can I get a Dad joke?
    ```

    This will now show a Dad joke.

    ![Dad joke](./assets/dadjoke.png)

And that was the Jokes MCP Server working in Microsoft Copilot Studio.

## ❌ Remove the Azure resources

To remove the Azure resources after finishing the lab, run the following command in the terminal:

```azurecli
azd down
```
This command will show you the resources that will be deleted and then ask you to confirm. Confirm with `y` and the resources will be deleted. This can take a couple of minutes, but at the end you will see a confirmation:

![resources deleted](./assets/azd-down-confirmation.png)

## 💡 Known issues and planned improvements

There are some known issues and planned improvements for MCP in Microsoft Copilot Studio. They are listed in [this Microsoft Learn article](https://aka.ms/mcsmcpdocs#known-issues--planned-improvements).

## 🗣️ Feedback

Hopefully you liked the lab. Please take the time to fill in our [feedback form](https://aka.ms/mcsmcp/lab/feedback) to tell us how we can improve!

## 🚀 Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## ™️ Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft 
trademarks or logos is subject to and must follow 
[Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general).
Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship.
Any use of third-party trademarks or logos are subject to those third-party's policies.

![Microsoft Copilot Studio ❤️ MCP](https://m365-visitor-stats.azurewebsites.net/?resource=https://github.com/microsoft/mcsmcp)
