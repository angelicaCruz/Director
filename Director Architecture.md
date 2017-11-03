# Director: Architecture #

![Directorxml](C:\Users\DataMesh\Documents\GitHub\Directorxml.png)

Director makes it possible to create a **Scenario** which is a PPT - like 3D scene. A Scenario is composed of **Roles** and **Stages**. 

##Roles

Roles represent the scene object. They are the equivalent of element is PPT. A role in Director is also called **asset role**. Every role has a behavior called **Action** and is managed in the Stage (state in the Finite State Machine). A role can several actions in the same state. 
It is mandatory for every role to have the following: 

- **Role ID**: must be unique as this identifies every role and actions depend on this.
- **Anchor ID**: lets the user position a specific role at the beginning of the scenario.

#### Types of Roles

1. **Asset Role** : a 3D model
2. **PicRole**: a picture
3. **Sound**
4. **Text** 

These objects can be found either  as **Assets in Storage** or **Local Resources** (what is the difference??)

## Actions

As mentioned before, Actions are the behavior attached to every existing role. An action is created inside a stage( state ) of a Finite State Machine and it may concern the creation or deletion of a role, appearance or disappearance of the role or the start of an animation of a specific role. Actions can also modify the position, scale and rotation of the role they are attached to. For every action, a role ID must be specified in order to create a relation between the role and the action it self. There are several actions that can be attached to a role: 

- **Create**: Download the role from its location and create an instance of the role in the Scenario
- **Clear**: Clears the specified role. 


- **Appear/Disappear**: Makes an existing role appear on/disappear from the scenario. 
- **InvokeFunction**
- **Play Animation**: Triggers an animation for the specified role ID. 
- **SwitchSceanrio**
- **Subtitles**
- **Tween**: Manipulates the role. This action influences the role's material, position, scale and rotation.

Some action may have **Delay** and **Duration** parameter. The first determines the delay(in real life seconds) of the action's execution while the latter is the length of the action. PlayAnimation is an action that uses Duration. 
There is a relation between the **Create** and **Appear** action. A role that is not yet created cannot appear and a created role cannot be seen if Appear action is not bound to the role. Thus, the act of creating an asset role doesn't determine the appearance of the role in Scenario. 



## Conditions

Conditions are part of the Finite State Machine and they determine if **transitions** from one state to another must be performed and thus, the change of scene. As seen in the class map, there are two types of conditions in Director:  

- **TimeEnd**: number of seconds during which the stage is active. The countdown starts the moment the stage is on the scene and when it reaches zero then the next stage is called and the current one is dismissed. 
- **NextStage**: waits for the click from the user. In HoloLens it is triggered by the **AirTap**.

When conditions are met, then transitions are made from one stage to another. These conditions are known to the server which will inform other devices of the changes that occurred.