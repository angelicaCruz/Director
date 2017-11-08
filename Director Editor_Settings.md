# Director Editor : Settings 

Director is METoolKit-based application so if you've tried METoolKit before, you may find similarities in the Project and Build settings of this project. 

Before proceeding, make sure you have the following: 

```
Unity 5.5 or later
Visual Studio 2017
Director Package with METoolkit
Mesh Expert Center
```

### Create a scene

1. In the **Project** panel, search for **MEHoloEntrance** prefab and drag it in the **Heirarchy**. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528888-5c3af0dc-c470-11e7-8e90-5d65fc6612d3.png">
</p>

2. Select MEHoloEntrance and go to the **Inspector** panel.  Add **App ID** and click on **Create All MEHolo Module** to create **MEHolo** game object that contains all Mesh Expert modules. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528890-5ca33b9c-c470-11e7-9e38-171c28943547.png">
<img src="https://user-images.githubusercontent.com/26377727/32528889-5c6da478-c470-11e7-8753-d9606084f104.png">
</p>

3. Search for **DirectoryManager** prefab and drag it in the Heirarchy. 

4. Create an empty game object and name it **Main App**. 

5. Select MainApp object and in the Inspector click on **Add Component** -> **New Script** and name it **MainAppScript**.

6. Open your **MainAppScript** and paste the code below.

   ```c#

   using System.Collections;
   using System.Collections.Generic;
   using UnityEngine;
   using Newtonsoft.Json;
   using DataMesh.AR;
   using DataMesh.AR.Director;
   using DataMesh.AR.Interactive;

   public class MainAppScript : MonoBehaviour
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

7. Save the scene to make the changes permanent. 

### Project and Build Settings

1. Open **Edit** -> **Project Settings** -> **Quality**.
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528870-58ad052c-c470-11e7-9522-2ba7f9ea1d6d.png" width="400">
</p>
2. In the **Inspector** panel go under **Windows Store** icon. Click on **Default** arrow and choose **Fastest**. You will see a green check right under Windows Store icon. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528871-5911faf4-c470-11e7-9a3d-3ceec20535e3.png" width="400">
</p>
3. Find **Other** under the same panel and change **V Sync Count** to **Don't Sync**. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528872-5965db56-c470-11e7-9c98-27aa0537cb03.png" width="400">
</p>

That's it for the Project Settings for this project. Below are the procedures to **Build** your project correctly. Our target device in our current scenario is the HoloLens. Once this procedure is done, other build for other devices will come easy. 

4. Open **File** -> **Build Settings**.

5. Add the scene you created with **Add Open Scene** button. Uncheck other scenes if there are any. 

6. Click on **Windows Store** and choose **Switch Platform**. If this is done correctly, you will see Unity icon beside Windows Store. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528874-599b8120-c470-11e7-8bbc-c6ea7a202f1e.png" width="400">
</p>

7. In the right side, do the following changes: 

   ```
   SDK: Universal10
   Target Device: HoloLens
   UWP Build Type: D3D
   Check Unity C# Project
   ```

8. Click on **Player Settings** -> **Other Settings**. Check **Virtual Reality Supported** and Windows Holographic will appear as the default SDK. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528882-5aea0a6a-c470-11e7-9cfe-aa1bfbe3b395.png" width="400">
</p>

9. Go to **Publishing Settings** -> **Capabilities** and check the following:

   ```
   InternetClient
   InternetClientServer
   PrivateNetworkClientServer
   WebCam
   SpatialPerception
   Microphone
   ```

10. Click **Build** button to start the process. Create a folder that will contain all build-related information and the VisualStudio solution that will be used to deploy the application on device. 

### Deploy on Device

1. Open the folder that contains build information and search for the VisualStudio solution and open it. 
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528883-5b20fe80-c470-11e7-9c9f-eefa304f7e41.png" width="400">
</p>

2. Connect your HoloLens with you Pc through USB cable for a faster deploy. 

3. In the panel above, do as follows: 

   ```
   Debug: Release
   x64: x86
   Local Machine: Device
   ```
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528884-5b54af50-c470-11e7-8822-0d68465e7451.png" width="400">
</p>

4. Press **ctrl + F5** or press the icon beside **Device**.

**Note**: It is possible to deploy through WI-FI. Just change **Local Machine: Remote Machine**. A window will appear and you will have to provide your HoloLens IP address in the **Address** section. You can find this address in your HoloLens. Go to **Settings** -> **Network & Internet** -> **Advance option** -> **Ipv4 address**.
<p align="center">
<img src="https://user-images.githubusercontent.com/26377727/32528885-5b966576-c470-11e7-81e8-223db0bd0847.png" width="400">
</p>
