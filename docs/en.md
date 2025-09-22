Welcome to the Progpoint manual. Here you will find everything you need to understand how to use the application and its functionalities.
# Getting Started with Progpoint

The latest version of Progpoint is available at [its website](https://progpoint.espi.top/).

> [!NOTE] Compile locally
>
> If you prefer, you can compile it from the main repository to run it locally.>
> To compile, you need at least NodeJS version 22.13.1 and npm version 10.9.2. Inside the `progpoint-app` folder, run the following commands:
>
> ```
> npm install
> npm run dev
> ```

Once the application starts, you will see the Agent Blueprints window, initially empty.
# Interfaces
## Agent Blueprints

You can add new nodes by dragging them from the accordions on the right, and you can select which Agent Blueprint to modify using the selector at the top right. The search box in the top-left corner lets you select which Agent Blueprint to edit, or create a new one.

To design blueprints, drag basic and stat nodes into the node map, and connect them to form agent progression designs. Agent instances will calculate their stats based on the values received by stat nodes. If multiple nodes of the same stat exist in a blueprint, the final value for that stat will be the sum of all its nodes.


> [!WARNING] Known issues
> Some stat nodes may duplicate or even triple. If, when instantiating agents, you see values that don’t match your design, delete the stat nodes from the related Agent Blueprint and place them again.
### Basic Nodes Accordion

Accordion that includes the basic nodes. With a blueprint open, you can drag them into the node map area to create new nodes:
- **Note Node**: A node with a text box to write notes about the blueprint. Every new Agent Blueprint includes a note node encouraging you to drag nodes from the accordions.
- **Parameter Node**: Represents one of the parameters defined in the parameters accordion. Used as input for function or math nodes to perform calculations.
- **Math Node**: Defines a calculation (addition, subtraction, multiplication, or division) between two input nodes, returning the result as output.
- **Function Node**: Represents a function previously defined in the Function Designer, taking an input value for X and returning the result of that function.
### Stats Accordion

Accordion that includes all the stats defined in the project. You can drag them into the node map to create stat instances in the currently open Agent Blueprint. If multiple nodes of the same stat exist in the blueprint, the final value for that stat will be the sum of all nodes. You can also create, modify, and delete stats, as well as define their mutability.
### Parameters Accordion

Accordion that appears when an Agent Blueprint is selected. It includes a button to create new parameters. Here you’ll also find all the parameters created for the selected blueprint, as well as the default values given when creating a new instance.
## Function Designer

In this interface, you can create mathematical functions. In the selector on the left, you can view the functions you have created, as well as create new ones. For the selected function, you can type in the upper-left text box the form it should take. Progpoint accepts simple single-variable functions, and if the function is valid, a preview will appear in the graph below.
## Agent Instantiator

In this interface, you can use previously designed Agent Blueprints to create agent instances for use in the simulator. Using the search bar at the top, you can search agent instances by name.

For each agent instance, you can modify the following values:
* **Parameters**: All parameters start with the initial values assigned in the Designer, but you can modify them as you like for each instance.
* **Agent Actions**: You can add actions to the instance for use in the simulator. The agent will attempt actions in order, starting from the top; if requirements are not met, it will try the next one.
* **Other actions**: You can change the blueprint from which the agent instance originates, duplicate it, or delete it if needed.
## Action Designer

In this interface, you can design the actions that agent instances use in the simulator. It includes an action search tool, which works the same as the one in the Instantiator. Each action is defined by the following values:

- **Cost Stat**: The stat consumed when using the ability.
- **Cost**: The value consumed by the action. It can be positive, negative, or 0.
- **Calculators**: Numerical factors that determine the action’s effectiveness, e.g., the damage it deals. For each calculator, you must specify:
  - **Source**: Whether the stat comes from the acting agent or the target agent.
  - **Stat**: The stat that provides the value to the calculation function.
  - **Function**: The calculation function.
  - **Type**: Determines whether the calculator’s effectiveness result is additive or multiplicative with respect to the others.



> [!NOTE] About calculators
> Calculators are processed in creation order, from top to bottom. The initial value of an action before any calculator is 0, so no multiplicative calculator will affect the value until the first additive calculator is applied.
## Simulator

In the simulator interface, you can define and create new simulations. When creating a simulation, you must set the following properties:
- **HP Stat**: The stat that determines whether an agent is incapacitated and can no longer fight.
- **Turn order**: Decides whether turn order is random or sorted by the value of a stat.

Once a simulation is created, you must assign agents to the ally and enemy teams and define simulation rules for them.

> \[!IMPORTANT] Simulation rules
> Simulation rules define the iterations of the simulations. For each rule, 50 battles are run.
>
Simulation rules have the following components:
- **Targets**: The agents affected by the rule.
- **Parameter**: The parameter modified by the rule. All target agents must have this parameter for it to be selectable.
- **Range**: The numeric range through which the rule iterates.
- **Increment**: The value by which the parameter increases in each iteration.

Once the simulation is ready, click **Batch Simulation** to run it. The results will appear below once finished.

> [!TODO] About the simulation
> When you click **Batch Simulation**, the application’s UI becomes unresponsive. Currently, if you open the console (usually with F12), you can view the simulation progress. A progress confirmation feature will be added in future updates.