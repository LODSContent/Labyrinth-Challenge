Module 00 - Prerequisites - Deployment and Setup

Introduction

In this Module, you'll deploy the Azure Services needed to run this workshop and get your local environment configured and ready. You will also learn about the structure of this workshop and get an overview of Multi-Agent Systems.

Learning Objectives and Activities

• Begin the deployment of the Azure Services
• Learn the structure and get an overview of this workshop
• Explore the core principals of multi-agent systems
• Complete the configuration of your local environment
• Compile and run the starter solution locally

Module Exercises

 Activity 1: Configure Workshop Environment:#activity-1-configure-workshop-environment
 Activity 2: Deploy Azure Services:#activity-2-deploy-azure-services
 Activity 3: Workshop Structure and Overview Session:#activity-3-workshop-structure-and-overview
 Activity 4: Configure Environment Variables:#activity-4-configure-environment-variables
 Activity 5: Compile and Run:#activity-5-compile-and-run

Activity 1 Configure Workshop Environment

Complete the following tasks in order to prepare your environment for this workshop.

Note: These pre-requisites are a hard requirement for successful completion of this workshop. If you do not have all three you will not be able to successfully complete this workshop.

Prerequisites

• Laptop or workstation with administrator rights (Alternatively you can run this workshop virtually in GitHub Codespaces:https://github.com/features/codespaces)
• Azure subscription with owner rights
• Subscription access to Azure OpenAI service. Start here to Request Access to Azure OpenAI Service:https://aka.ms/oaiapply. If you have access, see below for ensuring enough quota to deploy.

  #### Checking Azure OpenAI quota limits

  For this sample to deploy successfully, there needs to be enough Azure OpenAI quota for the models used by this sample within your subscription. This sample deploys a new Azure OpenAI account with two models, gpt-4o with 30K tokens per minute and text-3-large with 5k tokens per minute. For more information on how to check your model quota and change it, see Manage Azure OpenAI Service Quota:https://learn.microsoft.com/azure/ai-services/openai/how-to/quota

  #### Azure Subscription Permission Requirements

  This solution deploys a user-assigned managed identity:https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview and defines then applies Azure Cosmos DB and Azure OpenAI RBAC permissions to this as well as your own Service Principal Id. You will need the following Azure RBAC roles assigned to your identity in your Azure subscription or Subscription Owner:https://learn.microsoft.com/azure/role-based-access-control/built-in-roles/privileged#owner access which will give you both of the following.

  • Manged Identity Contributor:https://learn.microsoft.com/azure/role-based-access-control/built-in-roles/identity#managed-identity-contributor
  • Cosmos DB Operator:https://learn.microsoft.com/azure/role-based-access-control/built-in-roles/databases#cosmos-db-operator
  • Cognitive Services OpenAI User:https://learn.microsoft.com/azure/role-based-access-control/built-in-roles/ai-machine-learning#cognitive-services-openai-user

Get Started

You can choose from the following options to get started with the workshop.

GitHub Codespaces

You can run this sample app and workshop virtually by using GitHub Codespaces. The button will open a web-based VS Code instance in your browser:

 Open the template (this may take several minutes):

   Open in GitHub Codespaces（https://github.com/codespaces/badge.svg）:https://codespaces.new/AzureCosmosDB/banking-multi-agent-workshop?devcontainerpath=.devcontainer%2Fpython%2Fdevcontainer.json

 Move on to the Deployment:Module-00.md#deployment section.

Local Environment using VS Code Dev Containers

 Install Docker Desktop:https://docs.docker.com/desktop/, and VS Code:https://code.visualstudio.com/Download along with the Dev Containers extension:https://code.visualstudio.com/docs/devcontainers/tutorial#install-the-extension extension.

 Clone the repository and checkout the start branch:

   ```bash:
git clone https://github.com/AzureCosmosDB/banking-multi-agent-workshop/
   cd banking-multi-agent-workshop
   git fetch --all
   git checkout start
```
 Open the repository in VS Code and select Reopen in Container when prompted. When asked to Select a devcontainer.json file, select the Python Development Container.

4. Wait for the container to build and start. This is a one time operation and may take a few minutes.

5. Move on to the Deployment:Module-00.md#deployment section.

Local Environment without VS Code Dev Containers

 To run the workshop locally on your machine, install the following:

   • Docker Desktop:https://docs.docker.com/desktop/
   • Git:https://git-scm.com/downloads
   • Azure Developer CLI (azd):https://aka.ms/install-azd
   • Python 12+:https://www.python.org/downloads/
   • Your Python IDE or VS Code:https://code.visualstudio.com/Download with Python Extension:https://marketplace.visualstudio.com/items?itemName=ms-python.python
   • To build and run the frontend component, install Node.js:https://nodejs.org/en/download/ and Angular CLI:https://angular.dev/installation#install-angular-cli

 Clone the repository and navigate to the folder:

   ```bash:
git clone https://github.com/AzureCosmosDB/banking-multi-agent-workshop/
   cd banking-multi-agent-workshop
   git checkout start
```
 Move on to the Deployment:Module-00.md#deployment section.

Activity 2: Deploy Azure Services

Deployment

 From the terminal, switch to the start branch:

   ```bash:
git checkout start
```
 Navigate to the correct folder:

   ```bash:
cd python/infra
```
 Log in to Azure using AZD.

   ```bash:
azd auth login
```
 Provision the Azure services and deploy the application.

   ```bash:
azd up
```
This step will take approximately 10-15 minutes. If you encounter an error during step, first rerun azd up. This tends to correct most errors.

[!IMPORTANT]
If you encounter any errors during the deployment, rerun azd up to continue the deployment from where it left off. This will not create duplicate resources, and tends to resolve most issues.

 When the resources are finally deployed, you will see a message in the terminal like below:

```bash:
Deploying services (azd deploy)

  (✓) Done: Deploying service ChatServiceWebApi
  • Endpoint: https://ca-webapi-6xbkqp3ybtbuw.whitemoss-86b36485.eastusazurecontainerapps.io/

Do you want to add some dummy data for testing? (yes/no): y
```
 Press y to load the data for the workshop.


Activity 3: Workshop Structure and Overview Session

While the Azure Services are deploying we will have a presentation to cover on the structure for this workshop for today as well as provide an introduction and overview of multi-agent sytems.

Activity 4: Configure Environment Variables

When you deploy this solution it automatically injects endpoints and configuration values for the required resources into a .env file at root (python) folder.

But you will still need to install dependencies to run the solution locally.

 Navigate to the python folder of the project.
 Create and activate a virtual environment (Linux/Mac):

   ```shell:
python -m venv .venv
   source .venv/bin/activate
```
   For Windows:

   ```shell:
python -m venv .venv
   .venv\Scripts\Activate.ps1
   ```
 Install the required dependencies for the project.

   ```shell:
pip install -r ../src/app/requirements.txt
   ```
   Note: If getting requirements.txt file not found when using GitHub codespaces, please navigate to the src/app folder and run the command there  pip install -r requirements.txt

Activity 5: Compile and Run

Running the solution

 Navigate to the python folder of the project.
 Start the fastapi server.

   shell:
uvicorn src.app.bankingagentsapi:app --reload --host 0.0.0.0 --port 8000

The API will be available at http://localhost:8000/docs. This has been pre-built with boilerplate code that will create chat sessions and store the chat history in Cosmos DB.

Run the Frontend App locally

 Update the apiUrl values in frontend/src/environments/environment.ts file with the API endpoint (http://localhost:8000/)
 Open a new terminal, navigate to the frontend folder and run the following to start the application:

   ```sh:
npm install
   npm start
```
 Open your browser and navigate to <http://localhost:8000/>.

Run the Frontend App on Codespaces


 Open a new terminal, navigate to the frontend folder and run the following to start the application:

   ```sh:
npm install
   npm start
 ```  
 From the Ports tab:
    Right-click and select the Port Visibility option to set port ChatAPI (8000) as Public.
    For the port with the label Frontend app. Hover over the address and choose Open in Browser (second icon) to access the frontend application.

Lets try a couple of things:

• Try out the API by creating a chat session in the front end. This should return a response saying "Hello, I am not yet implemented".
• Navigate to the Cosmos DB account in the Azure portal to view the containers. You should see an entry in the Chat container. If you selected "yes" to the option during azd up, there will also be some transactional data in the OffersData, AccountsData, and Users containers as well.
• Take a look at the files in the src/app/services folder - these are the boilerplate code for interacting with the Cosmos DB and Azure OpenAI services.
• You will also see an empty file src/app/bankingagents.py as well as empty files in the src/app/tools and src/app/prompts folder. This is where you will build your multi-agent system!

Next, we will start building the agents that will be served by the API layer and interact with Cosmos DB and Azure OpenAI using LangGraph!

Deployment Validation

Use the steps below to validate that the solution was deployed successfully.

• [ ] All Azure resources are deployed successfully
• [ ] You can compile the solution in CodeSpaces or locally
• [ ] You can start the project and it runs without errors

Common Issues and Troubleshooting

 Errors during azd deployment:

• Service principal "not found" error.
  • Rerun azd up
• If you are running on Windows with Powershell, you may get:
  • "error executing step command 'deploy --all': getting target resource: resource not found: unable to find a resource tagged with 'azd-service-name: ChatServiceWebApi'"
  • This is likely because you have used Az CLI before, and have an old default resource group name cached that is different from the one specified during azd up.
  • To resolve this:
    • Delete .azure in the root folder and .azd folders in your home directory (C:\Users\<user name>).
    • Start again, but first set resource group explicitly. Replace <environment name> in the below with the name you intend to set for your environment:
      • azd env set AZURERESOURCE_GROUP rg-<environment name>
      • Then enter <environment name> when prompted:
        • Enter a new environment name: <environment name>
      • Run azd auth login again
      • Then run azd up again.

 Azure OpenAI deployment issues:

• Ensure your subscription has access to Azure OpenAI
• Check regional availability

 Python environment issues:

• Ensure correct Python version
• Verify all dependencies are installed



Success Criteria

To complete this Module successfully, you should be able to:

• Verify that all services have been deployed successfully.
• Have an open IDE or CodeSpaces session with the source code and environment variables loaded.
• Be able to compile and run the application with no warnings or errors.

Next Steps

Proceed to Creating Your First Agent

Resources

• azd Command Reference:https://learn.microsoft.com/azure/developer/azure-developer-cli/reference
• Semantic Kernel Agent Framework:https://learn.microsoft.com/semantic-kernel/frameworks/agent
• LangGraph:https://langchain-ai.github.io/langgraph/concepts/
• Azure OpenAI Service documentation:https://learn.microsoft.com/azure/cognitive-services/openai/
• Azure Cosmos DB Vector Database:https://learn.microsoft.com/azure/cosmos-db/vector-database

<details>
  <summary>If you prefer to run this locally on your machine, open this section and install these additional tools.</summary>

<br>

</details>

Module 01 - Creating Your First Agent

Introduction

In this Module, you'll implement your first agent as part of a multi-agent banking system implemented using either Semantic Kernel Agent Framework or LangGraph. You will get an introduction to Semantic Kernel and LangChain frameworks and their plug-in/tool integration with OpenAI for generating completions.

Learning Objectives and Activities

• Learn the basics for Semantic Kernel Agent Framework and LangGraph
• Learn how to integrate agent frameworks to Azure OpenAI
• Build a simple chat agent

Module Exercises

 Activity 1: Session on Single-agent architecture:#activity-1-session-on-single-agent-architecture
 Activity 2: Session on Semantic Kernel Agent Framework and LangGraph:#activity-2-session-on-semantic-kernel-agent-framework-and-langgraph
 Activity 3: Create Your Very First Agent:#activity-3-create-your-very-first-agent
4. Activity 4: Create a Simple Customer Service Agent:#activity-4-create-a-simple-customer-service-agent
5. Activity 5: Test your Work:#activity-5-test-your-work

Activity 1: Session on Single-agent architecture

In this session you will get an overview of Semantic Kernel Agents and LangGraph and learn the basics for how to build a chat app that interacts with a user and generations completions using an LLM powered by Azure OpenAI.

Activity 2: Session on Semantic Kernel Agent Framework and LangGraph

In this session, you will get a deeper introduction into the Semantic Kernel Agent Framework and LangGraph with details on how to implement plug-in or tool integration with Azure Open AI.

The following steps are completed in your IDE.

Project Structure

This solution is organized in the folders below within the /src folder

• /src The root folder for the solution. 
    • /app The folder for the application files.
        • bankingagentsapi.py This is the API front-end for this application
        • bankingagents.py This is where the agents are defined.
        • prompts This folder contains all of the prompty files which define each agent's behavior
        • services This folder contains the service layer wrappers for Azure Cosmos DB and Azure OpenAI Service
        • tools This folder contains the tool definitions for each of the agents in this application
    • /test This folder contains the python script to test our application

Here is what the structure of this solution appears like in VS Code. Spend a few moments to familiarize yourself with the structure as it will help you navigate as we go through the activities.

Solution Files（./media/module-01/solution-folder-files.png）


Activity 3: Create your very first agent

In this hands-on exercise, you will learn the basic elements of a LangGraph agent application and how to define and implement them.

LangGraph is a powerful extension of LangChain that allows you to create stateful, multi-agent workflows using graph-based execution. It helps define AI-driven workflows where multiple agents collaborate, passing state and decisions dynamically.

LangGraph is a directed graph where Nodes represent different, functions, agents or steps in the AI workflow. The Edges in the graph define the possible transitions between nodes and State represents the evolving data as the workflow executes.

The main components of a LangGraph app include:
• StateGraph - The core execution engine for defining and executing multi-step workflows.
• State (Memory) Management - For tracking progress, sharing information and chat history.
• Agents - Individual entities with decision making capabilities.
• Tools - Provide external capabilities.


Let's begin to create our first agent application.

To being, navigate to the src/app folder of your project.

Open the the empty bankingagents.py file.

Copy the following code into it.

```python:
import logging
import os
import uuid
from langchain.schema import AIMessage
from typing import Literal
from langgraph.graph import StateGraph, START, MessagesState
from langgraph.prebuilt import createreactagent
from langgraph.types import Command, interrupt
from langgraph.checkpoint.memory import MemorySaver
from src.app.services.azureopenai import model

localinteractivemode = False

logging.basicConfig(level=logging.ERROR)

PROMPTDIR = os.path.join(os.path.dirname(file), 'prompts')

load prompts

define agents & tools

define functions

define workflow
```
This code here is the basis upon which we will build our multi-agent application. Notice the comments. Each of these specify the core of how you build a multi-agent application in LangGraph. For the remainer of this module we will replace each of these with the sections below in order.


Prompts

Agent applications are powered by large language models or LLMs. Defining the behavior for an agent in a system powered by LLMs requires a prompt. This system will have lots of agents and lots of prompts. To simplify construction, we will define a function that loads the prompts for our agents from files.

In the bankingagents.py file, navigate to the # load prompts comment.

Replace the comment with the following:

```python:
def loadprompt(agentname):
    """Loads the prompt for a given agent from a file."""
    filepath = os.path.join(PROMPTDIR, f"{agentname}.prompty")
    print(f"Loading prompt for {agentname} from {filepath}")
    try:
        with open(filepath, "r", encoding="utf-8") as file:
            return file.read().strip()
    except FileNotFoundError:
        print(f"Prompt file not found for {agentname}, using default placeholder.")
        return "You are an AI banking assistant."  # Fallback default prompt
```
Agents & Tools

Agents are the heart of these applications. Below, we are going to create a ReAct Agent. ReAct, or Re-Act stands for, Reason and Act and is a specific type of agent that is what you will most often use in a multi-agent scenario like this one. 

In LangGraph there are different types of agents you can create, depending on your needs. These include:

| Agent Type | Best for |
|-|-|
| React Agent | Reasoning and decision making and tool use |
| Tools Agent | Direct function calling with structured APIs |
| Custom Agents| Full control over logic & multi-agent workflows |

In LangGraph, the definition of an agent includes any Tools it needs to do its job. This often involves retrieving some information or taking some action, like transfering execution to another agent (we will get into that soon). If an agent doesn't require any tools, this is defined as empty.

In our simple agent we are going to define a new React Agent as the coorindator for our app using a built-in function called, createreactagent(). Since this is our first agent, there are no tools to define for it so the tools we define for it will be empty. Notice that this agent also calls the function we defined above, loadprompt().


In the bankingagents.py file, navigate to the # define agents & tools comment.

Replace the comment with the following:

```python:
tools = []
coordinatoragent = createreactagent(
    model,
    tools=tools,
    statemodifier=loadprompt("coordinatoragent"),
)
```
Functions

Since LangGraph is a graph, the agents, which are comprised of prompts, tools, and functions are implemented as nodes. But humans are also a part of the workflow here so we need to define them as a node too. In our simple sample we have two nodes, one for the coordinator agent and one for the human.


In the bankingagents.py file, navigate to the # define functions comment.

Replace the comment with the following:

```python:
def callcoordinatoragent(state: MessagesState, config) -> Command[Literal["coordinatoragent", "human"]]:
    response = coordinatoragent.invoke(state)
    return Command(update=response, goto="human")


The humannode with interrupt function serves as a mechanism to stop
the graph and collect user input for multi-turn conversations.
def humannode(state: MessagesState, config) -> None:
    """A node for collecting user input."""
    interrupt(value="Ready for user input.")
    return None
```
Built-in Functions

Before we go any further we should cover a few new things you may have seen. LangGraph has a series of built-in functions that you will use when building these types of applications. The first you saw above when we defined our agent, createreactagent(). There are two more used above, Command() and interrupt(). Here is a short summary of built-in functions.


| Function | Purpose |
|-|-|
| createreactagent() | Create an agent that reasons and acts using tools dynamically. |
| interrupt(value) | Pauses execution and waits for external input. |
| Command(update, goto) | Updates the state and moves execution to the next node. |
| createopenaitoolsagent() | Create an agent that calls predefined tools when needed. |


Workflow

With our everything we need for our graph defined we are now ready to define the workflow for our graph.

In LangGraph, the, StateGraph is the execution engine where everything comes together. It defines the state that holds the information for the workflow, builds the workflow logic, and dynamically executes the workflow based upon the function outputs and logic defined in the graph.

The workflow below is defined with both, the addition of nodes that define who is doing the interacting, and an edge that defines a transition between the two.


In the bankingagents.py file, navigate to the # define workflow comment.

Replace the comment with the following:

```python:
builder = StateGraph(MessagesState)
builder.addnode("coordinatoragent", callcoordinatoragent)
builder.addnode("human", humannode)

builder.addedge(START, "coordinatoragent")

checkpointer = MemorySaver()
graph = builder.compile(checkpointer=checkpointer)
```
Defining Prompts

Before we are finished creating our first agent, we need to define its behavior.


In your IDE, navigate to the the src/app/prompts folder in your project.

Locate and open the empty coordinatoragent.prompty file.

Copy and paste the following text into it:

```code:
You are a Chat Initiator and Request Router in a bank.
Your primary responsibilities include welcoming users, and routing requests to the appropriate agent.
If the user needs general help, tell them you will be able to transfer to 'customersupport' for help when that agent is built.
If the user wants to open a new account or take our a bank loan, tell them you will be able to transfer to transfer to 'salesagent' when built.
If the user wants to check their account balance or make a bank transfer, tell them you will be able to transfer to transfer to 'transactionsagent' when built
You MUST include human-readable response.
```

Let's review

Congratulations, you have created your first AI agent!

We have:
• Used the createreactagent function from the langgraph.prebuilt module to create a simple "coordinator" agent. The function imports the Azure OpenAI model already deployed (during azd up) and defined in src/app/services/azureopenai.py and returns an agent that can be used to generate completions. 
• Defined a callcoordinatoragent function that invokes the agent and a humannode function that collects user input. 
• Created a state graph that defines the flow of the conversation and compiles it into a langgraph object.
• Added an in-memory checkpoint to save the state of the conversation.


We could run this and see it in action but before we do this, let's implement a second agent for our coorindator agent to transfer to. In this next activity, we are going to create a Customer Service Agent that our Coordinator Agent will transfer execution to on behalf of the user.


Activity 4: Create a Simple Customer Service Agent

In this activity, you will create a simple customer service agent that users interact with and generates completions using a large language model.

We've created a coordinator agent that can route requests to different agents. Now, let's create a simple customer service agent that can respond to user queries.

We'll cover tools in more detail in the next module, but we'll need to add our first tool (or rather a function that dynamically creates a tool) right here so that our coordinator agent can route requests to the customer service agent.


Create Agent Transfer Tool

To begin, navigate to the src/app/tools folder of your project.

Copy the following code into the empty coordinator.py file.

```python:
from colorama import Fore, Style
from langchaincore.tools import tool
from typing import Annotated
from langchaincore.tools.base import InjectedToolCallId
from langgraph.prebuilt import InjectedState
from langgraph.types import Command


def transfertoagentmessage(agent):
    print(Fore.LIGHTMAGENTAEX + f"transferto{agent}..." + Style.RESETALL)


def createagenttransfer(, agentname: str):
    """Create a tool that can return handoff via a Command"""
    toolname = f"transferto{agentname}"

    @tool(toolname)
    def transfertoagent(
            state: Annotated[dict, InjectedState],
            toolcallid: Annotated[str, InjectedToolCallId],
    ):
        """Ask another agent for help."""
        toolmessage = {
            "role": "tool",
            "content": f"Successfully transferred to {agentname}",
            "name": toolname,
            "toolcallid": toolcallid,
        }
        transfertoagentmessage(agentname)
        return Command(
            goto=agentname,
            graph=Command.PARENT,
            update={"messages": state["messages"] + [toolmessage]},
        )

    return transfertoagent
```

Next, navigate back to the bankingagents.py file.

At the top of the file, copy the following import statement:

```python:
from src.app.tools.coordinator import createagenttransfer
```

Next, within the same bankingagents.py file.

Locate this statement:


```python:
tools = []
```
Replace it with the following code:

```python:
coordinatoragenttools = [
    createagenttransfer(agentname="customersupportagent"),
]
```
On the line below, update the tools parameter in the coordinator agent creation.

Replace the value tools with the coordinatoragenttools definition. 

Your coordinator agent should now look like this:

```python:
coordinatoragent = createreactagent(
    model,
    tools=coordinatoragenttools,
    statemodifier=loadprompt("coordinatoragent"),
)
```
Define the Customer Support Agent

Now let's add the new customer support agent with an empty tool set, and a calling function.

Below the previous line of code, copy the following:

```python:
customersupportagenttools = []
customersupportagent = createreactagent(
    model,
    customersupportagenttools,
    statemodifier=loadprompt("customersupportagent"),
)
```
Next, locate the callcoordinatoragent() function on

Below this call, add a calling function for the customer support agent:

```python:
def callcustomersupportagent(state: MessagesState, config) -> Command[Literal["customersupportagent", "human"]]:
    response = customersupportagent.invoke(state)
    return Command(update=response, goto="human")
```
Define the Customer Service Agent Prompt

We are done building out our code for our customer service agent. Now, lets add a prompt for the customer support agent.

In your IDE, navigate to the src/app/prompts folder.

Locate the empty customersupportagent.prompty file. 

Copy and paste the following text into it:

```code:
You are a customer support agent that can give general advice on banking products and branch locations
If the user wants to make a complaint or speak to someone, ask for the user's phone number and email address,
and say you will get someone to call them back.
You MUST include human-readable response.

The coordinator agent's job in this multi-agent system is to handle routing to multiple different agents. However, to do that we need to give it instructions to do so. This is done in the coordinator agent's prompt. With our customer service agent, now fully defined, let's update the coordinator agent's prompty file so it can transfer to the customer support agent.
```

Update the Coorindator Agent Prompt

In your IDE, stay in the src/app/prompts folder.

Locate the coordinatoragent.prompty file.

Replace the text of the file with the text below (notice the difference in the third line between what is there now and the new text):

```code:
You are a Chat Initiator and Request Router in a bank.
Your primary responsibilities include welcoming users, and routing requests to the appropriate agent.
If the user needs general help, transfer them to the 'customersupportagent' agent.
If the user wants to open a new account or take our a bank loan, tell them you will be able to transfer to transfer to 'salesagent' when built.
If the user wants to check their account balance or make a bank transfer, tell them you will be able to transfer to transfer to 'transactionsagent' when built
You MUST include human-readable response.
```

Update our Workflow

Finally, we need to add the new customer support agent node to the StateGraph workflow.

In your IDE, navigate back to the bankingagents.py file.

Navigate towards the end of the file.

Locate this line of code, builder.addnode("coordinatoragent", callcoordinatoragent) 

Add the following line of code below it:

```python:
builder.addnode("customersupportagent", callcustomersupportagent)
```

Activity 5: Test your Work

With the activities in this module complete, it is time to test your work!

To do this, we are going to add this code to our bankingagents.py file.

This code defines a new function, interactivechat() that creates a message loop that invokes our StateGraph that we have defined in this file.

To being, navigate to the end of the bankingagents.py file.

Then paste the following code below all code in this file:

```python:
def interactivechat():
    threadconfig = {"configurable": {"threadid": str(uuid.uuid4()), "userId": "Mark", "tenantId": "Contoso"}}
    global localinteractivemode
    localinteractivemode = True
    print("Welcome to the single-agent banking assistant.")
    print("Type 'exit' to end the conversation.\n")

    userinput = input("You: ")
    conversationturn = 1

    while userinput.lower() != "exit":

        inputmessage = {"messages": [{"role": "user", "content": userinput}]}

        responsefound = False  # Track if we received an AI response

        for update in graph.stream(
                inputmessage,
                config=threadconfig,
                streammode="updates",
        ):
            for nodeid, value in update.items():
                if isinstance(value, dict) and value.get("messages"):
                    lastmessage = value["messages"][-1]  # Get last message
                    if isinstance(lastmessage, AIMessage):
                        print(f"{nodeid}: {lastmessage.content}\n")
                        responsefound = True

        if not responsefound:
            print("DEBUG: No AI response received.")

        # Get user input for the next round
        userinput = input("You: ")
        conversationturn += 1


if name == "main":
    interactivechat()
```
Ready to test


Try it out! 

In your IDE, run the following command in your terminal:

```bash:
python -m src.app.bankingagents
```
You should see the following output like below:

```code:
[DEBUG] Retrieved Azure AD token successfully using DefaultAzureCredential.
[DEBUG] Azure OpenAI model initialized successfully.
Loading prompt for coordinatoragent from prompts\coordinatoragent.prompty
Welcome to the single-agent banking assistant.
Type 'exit' to end the conversation.

You:
```

Input some text to the agent. 

Type the following text:


```code:
I want some help
```
You should see your query being routed to the customer support agent and a response generated:

```shell:
You: I want some help
transfertocustomersupportagent...
customersupportagent: You are now connected to our customer support agent. How can we assist you today?

You:
```
End the agent session by typing exit to end the application.



Validation Checklist

Your implementation is successful if:

• [ ] Your app compiles with no warnings or errors.
• [ ] Your agent successfully processes user input and generates and appropriate response.

Common Issues and Troubleshooting

 Issue 1: Nothing happens when I run bankingagents.py.
    • Confirm that all the code above has been accurately copy and pasted into the correct files.

 Issue 2: I get a ModuleNotFoundError: error when I run bankingagents.py.
    • Make sure that your venv is started in the terminal before running any python code.
    • Make sure that you installed all the python package requirements from Module 00


Module Solution

The following sections include the completed code for this Module. Copy and paste these into your project if you run into issues and cannot resolve.

<details>
  <summary>Completed code for <strong>src/app/bankingagents.py</strong></summary>

<br>

```python:
import logging
import os
import uuid
from langchain.schema import AIMessage
from typing import Literal
from langgraph.graph import StateGraph, START, MessagesState
from langgraph.prebuilt import createreactagent
from langgraph.types import Command, interrupt
from langgraph.checkpoint.memory import MemorySaver
from src.app.services.azureopenai import model
from src.app.tools.coordinator import createagenttransfer

localinteractivemode = False

logging.basicConfig(level=logging.ERROR)

PROMPTDIR = os.path.join(os.path.dirname(file), 'prompts')


def loadprompt(agentname):
    """Loads the prompt for a given agent from a file."""
    filepath = os.path.join(PROMPTDIR, f"{agentname}.prompty")
    print(f"Loading prompt for {agentname} from {filepath}")
    try:
        with open(filepath, "r", encoding="utf-8") as file:
            return file.read().strip()
    except FileNotFoundError:
        print(f"Prompt file not found for {agentname}, using default placeholder.")
        return "You are an AI banking assistant."  # Fallback default prompt


coordinatoragenttools = [
    createagenttransfer(agentname="customersupportagent"),
]
coordinatoragent = createreactagent(
    model,
    tools=coordinatoragenttools,
    statemodifier=loadprompt("coordinatoragent"),
)

customersupportagenttools = []
customersupportagent = createreactagent(
    model,
    customersupportagenttools,
    statemodifier=loadprompt("customersupportagent"),
)


def callcoordinatoragent(state: MessagesState, config) -> Command[Literal["coordinatoragent", "human"]]:
    response = coordinatoragent.invoke(state)
    return Command(update=response, goto="human")


def callcustomersupportagent(state: MessagesState, config) -> Command[Literal["customersupportagent", "human"]]:
    response = customersupportagent.invoke(state)
    return Command(update=response, goto="human")


The humannode with interrupt function serves as a mechanism to stop
the graph and collect user input for multi-turn conversations.
def humannode(state: MessagesState, config) -> None:
    """A node for collecting user input."""
    interrupt(value="Ready for user input.")
    return None


builder = StateGraph(MessagesState)
builder.addnode("coordinatoragent", callcoordinatoragent)
builder.addnode("customersupportagent", callcustomersupportagent)
builder.addnode("human", humannode)

builder.addedge(START, "coordinatoragent")

checkpointer = MemorySaver()
graph = builder.compile(checkpointer=checkpointer)


def interactivechat():
    threadconfig = {"configurable": {"threadid": str(uuid.uuid4()), "userId": "Mark", "tenantId": "Contoso"}}
    global localinteractivemode
    localinteractivemode = True
    print("Welcome to the single-agent banking assistant.")
    print("Type 'exit' to end the conversation.\n")

    userinput = input("You: ")
    conversationturn = 1

    while userinput.lower() != "exit":

        inputmessage = {"messages": [{"role": "user", "content": userinput}]}

        responsefound = False  # Track if we received an AI response

        for update in graph.stream(
                inputmessage,
                config=threadconfig,
                streammode="updates",
        ):
            for nodeid, value in update.items():
                if isinstance(value, dict) and value.get("messages"):
                    lastmessage = value["messages"][-1]  # Get last message
                    if isinstance(lastmessage, AIMessage):
                        print(f"{nodeid}: {lastmessage.content}\n")
                        responsefound = True

        if not responsefound:
            print("DEBUG: No AI response received.")

        # Get user input for the next round
        userinput = input("You: ")
        conversationturn += 1


if name == "main":
    interactivechat()
```
</details>

<details>
  <summary>Completed code for <strong>src/app/tools/coordinator.py</strong></summary>

<br>

```python:
from colorama import Fore, Style
from langchaincore.tools import tool
from typing import Annotated
from langchaincore.tools.base import InjectedToolCallId
from langgraph.prebuilt import InjectedState
from langgraph.types import Command


def transfertoagentmessage(agent):
    print(Fore.LIGHTMAGENTAEX + f"transferto{agent}..." + Style.RESETALL)


def createagenttransfer(, agentname: str):
    """Create a tool that can return handoff via a Command"""
    toolname = f"transferto{agentname}"

    @tool(toolname)
    def transfertoagent(
            state: Annotated[dict, InjectedState],
            toolcallid: Annotated[str, InjectedToolCallId],
    ):
        """Ask another agent for help."""
        toolmessage = {
            "role": "tool",
            "content": f"Successfully transferred to {agentname}",
            "name": toolname,
            "toolcallid": toolcallid,
        }
        transfertoagentmessage(agentname)
        return Command(
            goto=agentname,
            graph=Command.PARENT,
            update={"messages": state["messages"] + [toolmessage]},
        )

    return transfertoagent
```
</details>

<details>
  <summary>Completed code for <strong>src/app/prompts/coordinatoragent.prompty</strong></summary>

<br>

```code:
You are a Chat Initiator and Request Router in a bank.
Your primary responsibilities include welcoming users, and routing requests to the appropriate agent.
If the user needs general help, transfer them to the 'customersupportagent' agent.
If the user wants to open a new account or take our a bank loan, tell them you will be able to transfer to transfer to 'salesagent' when built.
If the user wants to check their account balance or make a bank transfer, tell them you will be able to transfer to transfer to 'transactionsagent' when built
You MUST include human-readable response.
```
</details>

<details>
  <summary>Completed code for <strong>src/app/prompts/customersupport_agent.prompty</strong></summary>

<br>

```code:
You are a customer support agent that can give general advice on banking products and branch locations
If the user wants to make a complaint or speak to someone, ask for the user's phone number and email address,
and say you will get someone to call them back.
You MUST include human-readable response.
```
</details>


Next Steps

Proceed to Connecting Agents to Memory

Resources

• LangGraph:https://langchain-ai.github.io/langgraph/concepts/
• Azure OpenAI Service documentation:https://learn.microsoft.com/azure/cognitive-services/openai/

Module 02 - Connecting Agents to Memory

Introduction

In this Module, you'll connect your agent to Azure Cosmos DB to provide memory for chat history and state management for your agents to provide durability and context-awareness in your agent interactions.


Learning Objectives and Activities

• Learn the basics for Azure Cosmos DB for storing state and chat history
• Learn how to integrate agent framworks to Azure Cosmos DB
• Test connectivity to Azure Cosmos DB works

Module Exercises

 Activity 1: Session Memory Persistence in Agent Frameworks:#activity-1-session-memory-persistence-in-agent-frameworks
 Activity 2: Connecting Agent Frameworks to Azure Cosmos DB:#activity-2-connecting-agent-frameworks-to-azure-cosmos-db
 Activity 3: Test your Work:#activity-5-test-your-work


Activity 1: Session Memory Persistence in Agent Frameworks

In this activity, you will get an overview of memory and how it works for Semantic Kernel Agents and LangGraph and learn the basics for how to configure and connect both to Azure Cosmos DB as a memory store for both chat history and/or state management.


Activity 2: Connecting Agent Frameworks to Azure Cosmos DB

Here you will learn how to initialize Azure Cosmos DB and integrate with LangGraph to provide persistent memory for chat history and state management.

The problem with our agents so far is that state is only maintained in memory and is lost when the agent graph is restarted. To solve this problem, we will use Azure Cosmos DB to store the state of the agent. Azure Cosmos DB is a distributed NoSQL database service in Azure. It is designed to for applications requiring low latency and high availability. It is especially adept at handling massive volumes of data with high-concurrency. And its schema-agnostic design makes it ideally suited for theset types of applications. We will also use Azure Cosmos DB to store chat history.

Adding state management using Cosmos DB is easy with the checkpointer plugin.

Checkpointer Plugin

The checkpointer plugin in LangGraph is a utility designed to facilitate the process of saving and restoring the state of an application at various points during its execution. This is particularly useful in multi-agent systems where maintaining consistent state across different agents and ensuring that progress can be resumed in case of failures or interruptions are critical.

Key Features of the Checkpointer Plugin:

• State Management: The checkpointer plugin allows developers to capture the current state of the agents and their interactions. This includes the data they are processing, their internal state, and any relevant context.
• Persistence: It provides mechanisms to persist this state to a durable storage medium, such as a database or file system. This ensures that the state can be reloaded even after a system crash or restart.
• Restoration: The plugin supports restoring the state to a previous checkpoint. This allows the system to resume operations from a known good state, reducing the need for reprocessing and minimizing downtime.
• Consistency: It ensures consistency across different agents by coordinating the checkpointing process. This is crucial in distributed systems where agents might be operating on different nodes or environments.
• Configuration: Developers can configure the frequency and conditions under which checkpoints are created. This flexibility allows for balancing between performance overhead and reliability.


Storing Agent State

Let's add the Checkpointer Plugin to our application.

To begin, navigate to the bankingAgents.py file.

Copy the code below to the top of the file with the other imports:

```python:
from langgraphcheckpointcosmosdb import CosmosDBSaver
from src.app.services.azurecosmosdb import DATABASENAME, checkpointcontainer, chatcontainer, updatechatcontainer, \
    patchactiveagent
```
In the same bankingagents.py file, scroll down to locate the following lines:

```python:
checkpointer = MemorySaver()
graph = builder.compile(checkpointer=checkpointer)
```
Then replace those two lines with the code below:

```python:
checkpointer = CosmosDBSaver(databasename=DATABASENAME, containername=checkpointcontainer)
graph = builder.compile(checkpointer=checkpointer)
```
From this point on, the agent will save its state to Azure Cosmos DB. The CosmosDBSaver class will save the state of the agent to the database represented by the global variable, DATABASENAME in the checkpointcontainer container.


Storing Agent Chat history

Next, we are going to modify the coordinator agent to store chat history.

Locate the following code in the bankingagents.py file:

```python:
def callcoordinatoragent(state: MessagesState, config) -> Command[Literal["coordinatoragent", "human"]]:
    response = coordinatoragent.invoke(state)
    return Command(update=response, goto="human")
```
Replace it with the following code:

```python:
def callcoordinatoragent(state: MessagesState, config) -> Command[Literal["coordinatoragent", "human"]]:
    threadid = config["configurable"].get("threadid", "UNKNOWNTHREADID")
    userId = config["configurable"].get("userId", "UNKNOWNUSERID")
    tenantId = config["configurable"].get("tenantId", "UNKNOWNTENANTID")

    logging.debug(f"Calling coordinator agent with Thread ID: {threadid}")

    # Get the active agent from Cosmos DB with a point lookup
    partitionkey = [tenantId, userId, threadid]
    activeAgent = None
    try:
        activeAgent = chatcontainer.readitem(
            item=threadid, 
            partitionkey=partitionkey).get('activeAgent', 'unknown')

    except Exception as e:
        logging.debug(f"No active agent found: {e}")

    if activeAgent is None:
        if localinteractivemode:
            updatechatcontainer({
                "id": threadid,
                "tenantId": "Contoso",
                "userId": "Mark",
                "sessionId": threadid,
                "name": "cli-test",
                "age": "cli-test",
                "address": "cli-test",
                "activeAgent": "unknown",
                "ChatName": "cli-test",
                "messages": []
            })

    logging.debug(f"Active agent from point lookup: {activeAgent}")

    # If active agent is something other than unknown or coordinatoragent, transfer directly to that agent
    if activeAgent is not None and activeAgent not in ["unknown", "coordinatoragent"]:
        logging.debug(f"Routing straight to last active agent: {activeAgent}")
        return Command(update=state, goto=activeAgent)
    else:
        response = coordinatoragent.invoke(state)
        return Command(update=response, goto="human")
```
Lastly, we will store chat history for the customer service agent as well.

Locate the following code in the bankingagents.py file:

```python:
def callcustomersupportagent(state: MessagesState, config) -> Command[Literal["customersupportagent", "human"]]:
    response = customersupportagent.invoke(state)
    return Command(update=response, goto="human")
```
Replace it with the following code:

```python:
def callcustomersupportagent(state: MessagesState, config) -> Command[Literal["customersupportagent", "human"]]:
    threadid = config["configurable"].get("threadid", "UNKNOWNTHREADID")
    if localinteractivemode:
        patchactiveagent(
            tenantId="Contoso", 
            userId="Mark", 
            sessionId=threadid,
            activeAgent="customersupportagent")

    response = customersupportagent.invoke(state)
    return Command(update=response, goto="human")
```
The patchactiveagent function is used to log or track which agent is currently active within a multi-agent LangGraph application. It typically records metadata such as the tenantId, userId, sessionId (or thread ID), and the name of the activeAgent. This is especially useful in local or interactive environments where you want visibility into which agent is handling a specific part of the conversation. 


Let's review

In this activity, we completed the following key steps:

• Stored the active agent in Cosmos DB:  
  We added logic to persist the current "active agent" in Azure Cosmos DB. Before routing, we check if an agent is already active—if so, the system routes the conversation directly to that agent without relying on further reasoning.

• Enabled persistent state and chat history:  
  We configured the application to store chat history and conversation state in Cosmos DB, ensuring the data persists beyond the current runtime session and can be retrieved across sessions or restarts.

• Patched the active agent after agent transfer:  
  After handing off to a new agent, we update the activeAgent field in the Cosmos DB Chat container. This ensures deterministic, turn-by-turn routing—especially when it's known which agent asked the last question.

Note: While it's technically possible to rely on the LLM to determine the next agent using reasoning alone, this approach is generally less reliable and may not be suitable for scenarios requiring consistency and control.


Activity 3: Test your Work

With the activities in this module complete, it is time to test your work!

Before testing, lets make a small amendment to your interactivechat() function in our bankingagents.py file to hardcode the thread ID. The thread ID is the unique identifier for the conversation state. Until now, we have not made use of it. In the change below we are going to hard code it to demonstrate how the conversation can be picked up later even when the application has stopped.

Within the bankingagents.py file locate the def interactivechat() function.

Immediately above the function declaration add the following line of code:

```python:
hardcodedthreadid = "hardcoded-thread-id-01"
```
Then replace the first line immediately within the function to this:

```python:
def interactivechat():
    threadconfig = {"configurable": {"threadid": hardcodedthreadid, "userId": "Mark", "tenantId": "Contoso"}}
```
Ready to test

Let's test our agents!

In your IDE, run the following command in your terminal:

```bash:
python -m src.app.bankingagents
```
Type the following text:

```code:
I want some help
```
You should see your query being routed to the customer support agent and a response generated:

```bash:
You: I want some help
transfertocustomersupportagent...
customersupportagent: Hi there! How can I assist you today? If you need help with opening a new account, taking out a loan, checking your account balance, making a transfer, or anything else, let me know!

You:
```
To prove that agent state is preserved we will shut down the agent. 

In the terminal type exit.

```code:
You: exit
```
Next, open your browser and find the Cosmos DB account you deployed in Module 0. 

Look for the Cosmos DB account in the resource group.

Navigate to Data Explorer within the Cosmos DB blade then locate the Chat container.

Open the Chat container. 

You should see the agent state and chat history stored there, with "customersupportagent" as the active agent.

TODO Note: I DO NOT SEE anything in Chat History container. Only the Chat container and inside ChatContainer I don't see any messages from the chat session itself, only a single item with an empty messages array. Also why is there a ChatHistory container in this database? Does this get used?

Navigate back to your terminal and restart the application.

```bash:
python -m src.app.bankingagents
```
Ask it for some help again. The coordinator agent should pick up the conversation where it left off and route straight to the customer support agent:

```bash:
Welcome to the single-agent banking assistant.
Type 'exit' to end the conversation.

You: I want some help
customersupportagent: Of course! Please let me know what kind of help you need. Are you looking to open a new account, take out a loan, check your account balance, make a transfer, or something else? I'm here to assist!

You:
```
You may also want to look at the checkpoints container in your Cosmos DB account. You should see the agent state stored there. There is much more data stored in this container, as it is not only maintaining the chat history, but also the state of the agent, and any other agent, including computations in between transfers. This allows for a richer conversational experience as the full agent state is remembered and checkpointed regularly. 

Validation Checklist

Your implementation is successful if:

• [ ] Your app compiles with no warnings or errors.
• [ ] Your agent successfully connects to Azure Cosmos DB.


Module Solution

The following sections include the completed code for this Module. Copy and paste these into your project if you run into issues and cannot resolve.

<details>
  <summary>Completed code for <strong>src/app/bankingagents.py</strong></summary>

<br>

```python:
import logging
import os
import uuid
from langchain.schema import AIMessage
from typing import Literal
from langgraph.graph import StateGraph, START, MessagesState
from langgraph.prebuilt import createreactagent
from langgraph.types import Command, interrupt
from langgraph.checkpoint.memory import MemorySaver
from src.app.services.azureopenai import model
from src.app.tools.coordinator import createagenttransfer
from langgraphcheckpointcosmosdb import CosmosDBSaver
from src.app.services.azurecosmosdb import DATABASENAME, checkpointcontainer, chatcontainer, updatechatcontainer, \
    patchactiveagent

localinteractivemode = False

logging.basicConfig(level=logging.ERROR)

PROMPTDIR = os.path.join(os.path.dirname(file), 'prompts')


def loadprompt(agentname):
    """Loads the prompt for a given agent from a file."""
    filepath = os.path.join(PROMPTDIR, f"{agentname}.prompty")
    print(f"Loading prompt for {agentname} from {filepath}")
    try:
        with open(filepath, "r", encoding="utf-8") as file:
            return file.read().strip()
    except FileNotFoundError:
        print(f"Prompt file not found for {agentname}, using default placeholder.")
        return "You are an AI banking assistant."  # Fallback default prompt


coordinatoragenttools = [
    createagenttransfer(agentname="customersupportagent"),
]
coordinatoragent = createreactagent(
    model,
    tools=coordinatoragenttools,
    statemodifier=loadprompt("coordinatoragent"),
)

customersupportagenttools = []
customersupportagent = createreactagent(
    model,
    customersupportagenttools,
    statemodifier=loadprompt("customersupportagent"),
)


def callcoordinatoragent(state: MessagesState, config) -> Command[Literal["coordinatoragent", "human"]]:
    threadid = config["configurable"].get("threadid", "UNKNOWNTHREADID")
    userId = config["configurable"].get("userId", "UNKNOWNUSERID")
    tenantId = config["configurable"].get("tenantId", "UNKNOWNTENANTID")

    logging.debug(f"Calling coordinator agent with Thread ID: {threadid}")

    # Get the active agent from Cosmos DB with a point lookup
    partitionkey = [tenantId, userId, threadid]
    activeAgent = None
    try:
        activeAgent = chatcontainer.readitem(
            item=threadid,
            partitionkey=partitionkey).get('activeAgent', 'unknown')

    except Exception as e:
        logging.debug(f"No active agent found: {e}")

    if activeAgent is None:
        if localinteractivemode:
            updatechatcontainer({
                "id": threadid,
                "tenantId": "Contoso",
                "userId": "Mark",
                "sessionId": threadid,
                "name": "cli-test",
                "age": "cli-test",
                "address": "cli-test",
                "activeAgent": "unknown",
                "ChatName": "cli-test",
                "messages": []
            })

    logging.debug(f"Active agent from point lookup: {activeAgent}")

    # If active agent is something other than unknown or coordinatoragent, transfer directly to that agent
    if activeAgent is not None and activeAgent not in ["unknown", "coordinatoragent"]:
        logging.debug(f"Routing straight to last active agent: {activeAgent}")
        return Command(update=state, goto=activeAgent)
    else:
        response = coordinatoragent.invoke(state)
        return Command(update=response, goto="human")


def callcustomersupportagent(state: MessagesState, config) -> Command[Literal["customersupportagent", "human"]]:
    threadid = config["configurable"].get("threadid", "UNKNOWNTHREADID")
    if localinteractivemode:
        patchactiveagent(
            tenantId="Contoso",
            userId="Mark",
            sessionId=threadid,
            activeAgent="customersupportagent")

    response = customersupportagent.invoke(state)
    return Command(update=response, goto="human")


The humannode with interrupt function serves as a mechanism to stop
the graph and collect user input for multi-turn conversations.
def humannode(state: MessagesState, config) -> None:
    """A node for collecting user input."""
    interrupt(value="Ready for user input.")
    return None


builder = StateGraph(MessagesState)
builder.addnode("coordinatoragent", callcoordinatoragent)
builder.addnode("customersupportagent", callcustomersupportagent)
builder.addnode("human", humannode)

builder.addedge(START, "coordinatoragent")

checkpointer = CosmosDBSaver(databasename=DATABASENAME, containername=checkpointcontainer)
graph = builder.compile(checkpointer=checkpointer)
hardcodedthreadid = "hardcoded-thread-id-01"


def interactivechat():
    threadconfig = {"configurable": {"threadid": hardcodedthreadid, "userId": "Mark", "tenantId": "Contoso"}}
    global localinteractivemode
    localinteractivemode = True
    print("Welcome to the single-agent banking assistant.")
    print("Type 'exit' to end the conversation.\n")

    userinput = input("You: ")
    conversationturn = 1

    while userinput.lower() != "exit":

        inputmessage = {"messages": [{"role": "user", "content": userinput}]}

        responsefound = False  # Track if we received an AI response

        for update in graph.stream(
                inputmessage,
                config=threadconfig,
                streammode="updates",
        ):
            for nodeid, value in update.items():
                if isinstance(value, dict) and value.get("messages"):
                    lastmessage = value["messages"][-1]  # Get last message
                    if isinstance(lastmessage, AIMessage):
                        print(f"{nodeid}: {lastmessage.content}\n")
                        responsefound = True

        if not responsefound:
            print("DEBUG: No AI response received.")

        # Get user input for the next round
        userinput = input("You: ")
        conversationturn += 1


if name == "main":
    interactivechat()
```

</details>

Resources

• LangGraph:https://langchain-ai.github.io/langgraph/concepts/
• Azure OpenAI Service documentation:https://learn.microsoft.com/azure/cognitive-services/openai/
• Azure Cosmos DB Vector Database:https://learn.microsoft.com/azure/cosmos-db/vector-database