# Director Editor

Director Editor gives non-developer clients to create their own **Scenario** without having to write code. 

**Scenario** is a Unity scene that looks like **PPT**. Every scenario is made of **roles** and **stages**.  The first ones are the objects in scene (elements in PPT) and the latter are the stages of the **Finite State Machine(FSM)**. Stages contain **actions** that are related to roles such as movements and material-related operations. They also contain the conditions that will determine the **transitions** from one stage to another. 
In Director Editor there are two main types of conditions: time and user click.

## Creating a Scenario## 

As mentioned before, a scenario is a set of roles and stages. Thus, these elements must be created. 

Models and animations must be already in Unity. Of course, you must also have downloaded the Director package(reference). In using Director Editor, you are also using Finite State Machines in order to manage the stages and the transitions. DataMesh offers functions(??) to create roles and manage actions(transform, material and animations). There are also functions(??) to manage transitions(TimeEnd and NextStage.)

### Get Started ### 

If you are familiar with MeshExpert, the fist steps are basically the same as the first steps when creating a MeshExpert application. (???)

1. Open Unity, drag **Director package** under **Assets**. 

2. Find **MEHoloEntrance** and drag it on the **Heirarchy**.

3. Add the **App ID** and select **Create All Module**

4. Fine **Director Manager** prefab and add it on the Heirarchy.

5. Create an empty game object and name it **MainApp**. Create the component MainApp(script) with the code below:

   ```c#
   using System.Collections;
   using System.Collections.Generic;
   using UnityEngine;
   using Newtonsoft.Json;
   using DataMesh.AR;
   using DataMesh.AR.Director;
   using DataMesh.AR.Interactive;

   public class MainApp : MonoBehaviour
   {
       private DirectorManager directorManager;
       private MultiInputManager inputManager;

       // Use this for initialization
       void Start()
       {
           StartCoroutine(WaitForInit());
       }

       private IEnumerator WaitForInit()
       {
           MEHoloEntrance entrance = MEHoloEntrance.Instance;
           while (!entrance.HasInit)
           {
               yield return null;
           }
           directorManager = DirectorManager.Instance;
           directorManager.Init();
           directorManager.TurnOn();
       }
    }
   ```

6. Set the project and build it. (reference to MeshExpert project and buildsettings.)

### Finite State Machine ###

Finite State Machine in Director's case helps to manage stages and transitions without having to write a code. 
Have in mind that roles are also managed with FSM as they are inside the stages.

Create your FSM with the following steps.

1. Under Assets and create a FSM.(picture)
   Right click under Assets. Select **Create-> Unity Coding -> ICode -> StateMachine**. 
2. On the FSM window, right click to create a state. (picture) What to do insert in the stages will be discussed later.
3. To create transition between two stages(states), right click on the the state and select **Make Transition**. Make sure that the stages are in the right order when creating transitions. 



### Stages: Role, Actions and Conditions ###

Stages represent the container of actions that are related to roles, events that trigger animations and conditions that determine transition. Stages have name and description which can be optional. 

#### Roles ####

Roles are the scene objects. Unlike the normal Unity scene, objects do not need to be dragged on the scene and they only need to exist as a **resource asset** in Unity. An asset role can be a 3d model, a text, a picture or a sound.
We suggest to create the **asset role** in the first stage of the FSM. The creation of asset roles does determine the automatic appearance of the role in the scene.  Follow the steps below to create an asset role in you scenario.

1. Chose a stage and in the **Inspector** panel, information about the stage will appear. (picture) There is the **Actions** panel which will contain your desired action. Select **(+)** to add an action. From the menu, select **DataMesh->Director->CreateAssetRole**. In the Inspector panel, you will now see the newly added action. 
   In creating an asset role there numerous parameters that can be modified but the most important among them are: 


   - **AssetLocation**: determines where the roles come from. Asset in Storage means that the asset 				is Unity's list of resources while Local Resources means (..??..)

   - **Role ID**: determines the roles unique name in the scenario. The same resource can be used to 		create different asset roles as long ad the roles have different names. 

   -  **Anchor ID**: determines the anchor that is related to the asset role that is being created. 			Select the button to choose which anchor to use if there are already existing anchors, otherwise click on "Click to create a new variable[FsmObject]" to create a new anchor. It will appear under the "Variables" list in the FSM window. The same anchor can be used for different roles but have in mind that roles sharing the same will share the same position. 

   - **Need to Destroy After Stage Exit** : if checked, the role object will de destroyed after the stage transition and thus, will not be seen anymore on the scene.

     (picture: create asset role)

   This step must be done for every new asset role 


2.  Every created asset roles does not appear automatically on the scene and their appearance is under the scene creator's control. Therefor, asset roles can appear in any scene and stage. To make an asset role appear, click **(+)** in the Actions panel then select **DataMesh->Director->AddAppearanceAction**. In the **Role Id** section, add the desired asset role ID. 
   (picture add action)
3.  To add more actions to an asset role, repeat step two and choose the action you desire to add. 

#### Actions ####

Actions determine the behavior of a the role they are attached to. There are different types of actions that can be used in Director. 

- **Create/Clear**: create/clear an asset role.


- **Appear/Disappear**: makes the specified role appear or disappear on/from the scene.
- **Play Animation**: plays a specific role animation during a stage. 
- **Tween Action**: this type of action manipulates the asset role's position, rotation, scale and material.

Some action have **Delay** and **Duration** section. The firs one determines the delay in real seconds of the action's execution while the latter determines the the length of the action. Actions are executed accordingly to the way they are listed on the action list.

(picture list of action, delay and duration)

#### Conditions ####

Conditions help determine if a transition has to be made from one stage to another. If the specified condition is satisfied then, a transition is performed and the scene will be occupied by the roles and actions in the new stage. Conditions are always related to a transition. (picture)

In Director, we have a time related condition(**EndTime**) and user-action related condition(**NextStage**). EndTime uses the creator defined number of seconds to determine how long a certain stage must occupy the scenario. The countdown starts the moment the stage is on the scene and when it reaches zero then the next stage is called and the current one is dismissed. When using this type of condition, **Delay** and **Duration** parameter of certain actions must be considered and respected. Thus, the length of seconds for the stage must not be lesser that the sum of all Delay and Duration of the actions.
NextStage in the other hand gives more control of the transitions since it is based on the click performed by the user. In HoloLens, click is equivalent to the AirTap.

To add a condition, in the Inspector find **Actions->Conditions**. Select **(+)** and then **DataMesh->Director**.

(picture how to add condition, list of condition)

#### From FSM to Json file####

After finishing your FSM, save it. In order to use you FSM with **DirectorManager** you have to create the Json file from your FSM. 

1. Find you FSM and perform right click on it.

2. Select **DataMesh->Director->Parse Data from State Machine**.(picture)

3. Go to the **Console** window and if step two is successful there will be a debug message with reports about the FSM.(picture debug)

4. Leave Unity and then get back again to make the operation effective. 

5. Find the Json file of your FSM and then drag it on **DirectorManager->Test Scripts**.

6. Press play to  try and see how your FSM is working. 

   ​