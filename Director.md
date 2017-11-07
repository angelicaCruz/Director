# Director

## Overview	

![Directorxml](C:\Users\DataMesh\Documents\GitHub\Directorxml.png)

  ###Contents

- **Scenarios**
  Director contains a collection of scenarios created with Director Editor. A scenario is PPT-like 3D scene with its roles and stages.
  - **Roles**: these are game objects that are created and manipulated in different stages. A role can be 	     		a 3D model, an image, a text or even a sound.  Roles are not stored in the server therefor, roles exist only inside the device itself. 
  - **Actions**: behaviors that are related to different roles. They can be performed in different stages of 		a Scenario.
  - **Stages**: states of a FSM. They contain the list of actions related to different roles and conditions to	       be satisfied to perform a transition.
- **Finite State Machine **
  Handles the transition between different stages of a scenario. There can be several stages and there must be one condition to be satisfied to trigger a transition. 
- **UI**
  The application is given a straight forward user-interface to make it user friend. The user- interface is based on HoloLens basic interactions such as Gaze and AirTap. When the application starts, the user is presented a button that addresses which will bring the scenario selection menu. UI is also used to place and manipulate anchors in the scene. 
- **Server Support**
  Stages of the FSM are stored in a server which communicate with connected devices. When a transition is performed, the server broadcasts a signal to every connected devices so that they can perform stage transition in their own.
- **METoolKit** 
  METoolKit serves as the starting point for Director.
- **ICode**
  A Unity extension that helps create and handle FSM through a visual solution. 