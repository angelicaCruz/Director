# Director Editor

## Scenario 

To know more about Director's Scenario, go on (reference to Director Overview). Always remember that Scenario is the container of all role and stages. 
With Director Editor it is possible to create different Scenarios while Director can have several Scenarios and user can choose which one to use. 

### Creating a Finite State Machine

The FSM is the main element of every Scenario as it manages not only the transitions but also the stages that contain role - related actions such as: 

```
Create
Clear
Appear
Disapper
```

1. In the Project Panel, go to **Assets -> Director Editor -> Data**. This is not mandatory but it is a good way to easily find you FSM and its Json file.

2. Right click and then **Create** -> **Unity Coding** -> **ICode** -> **State Machine**. 
   (sc1)

3. Create the corresponding Json file your FSM. Right click on your FSM and choose **DataMesh** -> **Director** -> **Parse Data From StateMachine**. 
   (sc2)

4. You will not see the Json file immediately. You have to leave Unity window and get back to it. The Json file will appear. 

5. Find your FSM Json file and in the Heirarchy select **DirectorManager**. Drag you FSM Json file in **Test Scripts** in the Inspector panel. 
   Below is a sample Debug messages of a successful FSM Json file creation

   (sc3)

   **Note**: for every changes you make on your FSM you have to repeat the 5 steps listed above to make 
   ​	   changes(stage addition or stage changes) effective. 

6. To create a stage, double click on your FSM and the an FSM window will appear. Right click on the window and select **Create State**.  We suggest to have **Start/Create** and **End** stages. Put in the first stage create actions and put nothing in the latter. You can have as many stages as you need, just be organized. 
   (sc4)

7. To create a **transition**, right click on the state and select **Make Transition**. 

### Creating a Role

Unlike any Unity scene, there is no need to drag objects on the scene. The creation, appearance and disappearance of role is managed by the FSM. 

1. As suggested above, click on the **Start/Create** state. In the Inspector panel find **Actions** and click **( + )** button to add an action. 
2. Select **DataMesh** -> **Director** -> **Create( ... )**. Choose the creation action accordingly to the type of your action. **AssetRole** is for 3D models, **PicRole** is for image type role, **SoundRole** is for audio clips and **TextRole** is for text type roles. 
3.  After adding the action, a panel related to that action will appear in the Inspector panel. 
   (sc7)
4. Click on **Asset Location** to choose from where the application will download the assets from. Click on **Asset** to choose which asset to use. There are two locations to choose from: **Local Resource** and **Asset In Storage**. The first one will create roles from the objects inside **Resources** folder in Unity while the latter will download Asset bundle form DataMesh cloud. If you want to use your own models, choose the firs one making sure you have the Resources folder and your models are in it.
5. Add **Role Id**. A different Id must be given to different roles as actions need a Role Id to be related to a specific role. 
6. Add **Anchor Id**. Click on the button and **Click to create new variable** to create a new anchor variable. It will show on you FSM window under **Variables**.  Make sure that different roles have different anchors. Two roles sharing the same anchor id won't create any error during the application's execution but will give you visual problems as two roles will share the same position. Have in mind that in the beginning of the application, the user will be asked to position the anchors of the roles.  
   ( sc8.1 sc8)
   **Note**: Create action does not imply the immediate appearance of a role in the scenario. You need to add **Appearance** action. 

### Adding an Action 

An action is a behavior added to a specific role. An action can be : 

```
Create: to create an asset role
Clear: to delete a specific role
Appear: to make a role appeaer in a specific stage of the Scenario
Disappear: to make a role disappear from the Scenario
Play Animation: triggers an animation for a specific role
Tween Action: manipulates the role's material, transform(scale, position and rotation)
```

1. In your FSM window select any state, under the **Actions** list, select **( + )**  button. 
2. Select **DataMesh** -> **Director** -> **Add( ... )**.
   (sc9)
3. Add **Role Id**. This value must the id of the role you want to bind the action to. Aside from Role Id, **Delay** and **Duration** are frequently used. The first one is the number of real-time seconds after which the action will start. The second on the other hand is length of the whole action. 
   (sc10)

### Adding Transitions and Conditions

**Transitions** are arrows that start from one stage and end pointing to the next stage. They are performed when **Conditions** are satisfied. 

1. Select any state, right click and choose **Make Transition**. This will create automatically a transition both in the FSM window and in the Inspector panel of the state. 
   (sc11)
2. To add a Condition, in the Inspector panel of the selected stage find **Conditions** list and click **( + )**. Select **DataMesh** -> **Director**. We suggest to choose between **NextStage** and **TimeEnd** as they the stable choices. The first one is a user dependent trigger and it is based on the AirTap event coming from the user. The second one instead, is basically a timer set by the developer and when this timer reaches 0, then the transition is performed. 
   In using TimeEnd, Delay and Duration must be considered. Thus, TimeEnd must not be inferior to both of the mentioned variables from the action's panel. 
   (sc12).

