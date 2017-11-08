# Director Editor
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32530278-1c555bc6-c478-11e7-9135-78db0cf8654a.png">
</p>

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
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528893-5d4715f0-c470-11e7-83ba-aa70dc7aaac7.png">
</p>

3. Create the corresponding Json file your FSM. Right click on your FSM and choose **DataMesh** -> **Director** -> **Parse Data From StateMachine**. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32529464-ba4f160a-c473-11e7-8c88-4449c1010070.png">
</p>

4. You will not see the Json file immediately. You have to leave Unity window and get back to it. The Json file will appear. 

5. Find your FSM Json file and in the Heirarchy select **DirectorManager**. Drag you FSM Json file in **Test Scripts** in the Inspector panel. Below is a sample Debug messages of a successful FSM Json file creation
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32531603-aeea1d08-c47f-11e7-8fda-4c558279edfc.png">
<img src="https://user-images.githubusercontent.com/26377727/32528895-5dad3a9c-c470-11e7-94da-a9fc3650b451.png">
</p>

   **Note**: for every changes you make on your FSM you have to repeat the 5 steps listed above to make 
   ​	   changes(stage addition or stage changes) effective. 

6. To create a stage, double click on your FSM and the an FSM window will appear. Right click on the window and select **Create State**.  We suggest to have **Start/Create** and **End** stages. Put in the first stage create actions and put nothing in the latter. You can have as many stages as you need, just be organized. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528896-5de31518-c470-11e7-84df-8fc89ebea39d.png">
</p>

7. To create a **transition**, right click on the state and select **Make Transition**.
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528897-5e1c89f6-c470-11e7-94b8-a31756c17f74.png">
</p>

### Creating a Role

Unlike any Unity scene, there is no need to drag objects on the scene. The creation, appearance and disappearance of role is managed by the FSM. 

1. As suggested above, click on the **Start/Create** state. In the Inspector panel find **Actions** and click **( + )** button to add an action. 
2. Select **DataMesh** -> **Director** -> **Create( ... )**. Choose the creation action accordingly to the type of your action. **AssetRole** is for 3D models, **PicRole** is for image type role, **SoundRole** is for audio clips and **TextRole** is for text type roles. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528898-5e522dcc-c470-11e7-95f3-734be850055f.png">
</p>

3.  After adding the action, a panel related to that action will appear in the Inspector panel. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528899-5eac72f0-c470-11e7-92bb-b3b82ee39c3d.png">
</p>

4. Click on **Asset Location** to choose from where the application will download the assets from. Click on **Asset** to choose which asset to use. There are two locations to choose from: **Local Resource** and **Asset In Storage**. The first one will create roles from the objects inside **Resources** folder in Unity while the latter will download Asset bundle form DataMesh cloud. If you want to use your own models, choose the firs one making sure you have the Resources folder and your models are in it.
5. Add **Role Id**. A different Id must be given to different roles as actions need a Role Id to be related to a specific role. 
6. Add **Anchor Id**. Click on the button and **Click to create new variable** to create a new anchor variable. It will show on you FSM window under **Variables**.  Make sure that different roles have different anchors. Two roles sharing the same anchor id won't create any error during the application's execution but will give you visual problems as two roles will share the same position. Have in mind that in the beginning of the application, the user will be asked to position the anchors of the roles.  
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528864-5779933c-c470-11e7-91b3-b6e636578823.png">
<img src="https://user-images.githubusercontent.com/26377727/32528865-57aa6688-c470-11e7-854b-b10780f84de8.png">
</p>

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
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528866-57e3106e-c470-11e7-85e3-31bb0d5abb20.png">
</p>

3. Add **Role Id**. This value must the id of the role you want to bind the action to. Aside from Role Id, **Delay** and **Duration** are frequently used. The first one is the number of real-time seconds after which the action will start. The second on the other hand is length of the whole action. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528867-5817ab26-c470-11e7-9def-978b0626930b.png">
</p>

### Adding Transitions and Conditions

**Transitions** are arrows that start from one stage and end pointing to the next stage. They are performed when **Conditions** are satisfied. 

1. Select any state, right click and choose **Make Transition**. This will create automatically a transition both in the FSM window and in the Inspector panel of the state. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528868-58482210-c470-11e7-9ff0-969e8f7963d3.png">
</p>

2. To add a Condition, in the Inspector panel of the selected stage find **Conditions** list and click **( + )**. Select **DataMesh** -> **Director**. We suggest to choose between **NextStage** and **TimeEnd** as they the stable choices. The first one is a user dependent trigger and it is based on the AirTap event coming from the user. The second one instead, is basically a timer set by the developer and when this timer reaches 0, then the transition is performed. 
   In using TimeEnd, Delay and Duration must be considered. Thus, TimeEnd must not be inferior to both of the mentioned variables from the action's panel. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528869-587b0c20-c470-11e7-87b6-d017f3072058.png">
</p>

